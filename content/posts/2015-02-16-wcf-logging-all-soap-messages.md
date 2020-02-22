---
author: "Russell Patterson"
date: 2015-02-16 00:18:55+00:00
draft: false
title: 'WCF: Logging All SOAP Messages'
url: /2015/02/wcf-logging-all-soap-messages/
categories:
- Technical
- Windows Communication Foundation
---

Do you want to know what is actually in that SOAP message that your Windows Communication Foundation service is sending? Well, look no further. It's actually quite simple to output the XML that is being created.

First, there are a couple classes that need to be added to your service project (or a separate project). The first of these is perhaps the most important, which is the message inspector that is used to do the actual logging, etc.


    
    
    public class LoggingMessageInspector : IDispatchMessageInspector
    {
        public object AfterReceiveRequest(ref Message request, IClientChannel channel, InstanceContext instanceContext) 
        {
            // Log here (request.ToString();)
            return null;
        }
    
        public void BeforeSendReply(ref Message reply, object correlationState)
        {
            // Log here (reply.ToString();)
        }
    }
    



Next, we'll create a behavior that uses this inspector.


    
    
    public class LoggingBehavior : IEndpointBehavior
    {
        public void AddBindingParameters(ServiceEndpoint endpoint, BindingParameterCollection bindingParameters)
        {
        }
    
        public void ApplyClientBehavior(ServiceEndpoint endpoint, ClientRuntime clientRuntime)
        {
            throw new Exception("Only for server side");
        }
    
        public void ApplyDispatchBehavior(ServiceEndpoint endpoint, EndpointDispatcher endpointDispatcher)
        {
            var inspector = new LoggingMessageInspector();
            endpointDispatcher.DispatchRuntime.MessageInspectors.Add(inspector);
        }
    
        public void Validate(ServiceEndpoint endpoint)
        {
        }
    }
    



Now we'll create a Behavior Extension that uses the behavior we created.


    
    
    public class LoggingBehaviorBehaviorExtensionElement : BehaviorExtensionElement
    {
        protected override object CreateBehavior()
        {
            return new LoggingBehavior();
        }
    
        public override Type BehaviorType
        {
            get { return typeof(LoggingBehavior); }
        }
    }
    



Finally, we have to set up the behavior extension in the web.config so that the service uses it.

1. Assuming that there is already an element in the <system.serviceModel><services>, change the appropriate element to have a behaviorConfiguration="LoggingBehavior".

2. Still under <system.serviceModel>, add an element under <behaviorExtensions> with the name "loggingBehavior" and the type pointing to the full namespace of our LoggingBehaviorExtensionElement.

3. Again, still under <system.serviceModel>, add a  element under <behaviors>/<endpointBehaviors> with the name "LoggingBehavior" and an element within it called "loggingBehavior".

Here's the full XML that we're adding to the web.config:
 

    
    
    <configuration>
        <system.serviceModel>
            <services>
                <service name="FULL-NAMESPACE-TO-SERVICE-IMPLEMENTATION" behaviorConfiguration="StandardBehavior">
                    <endpoint address="" behaviorConfiguration="LoggingBehavior" binding="basicHttpBinding" 
    						contract="FULL-NAMESPACE-TO-SERVICE-CONTRACT" />
                </service>
            </services>
            <extensions>
                <behaviorExtensions>
                    <add name="loggingBehavior" type="FULL-NAMESPACE.LoggingBehaviorBehaviorExtensionElement" />
                </behaviorExtensions>
            </extensions>
            <behaviors>
                <endpointBehaviors>
                    <behavior name="LoggingBehavior">
                        <loggingBehavior />
                    </behavior>
                </endpointBehaviors>
            </behaviors>
        </system.serviceModel>
    </configuration>
    



That's all there is to it. You can add code to log using your favorite logger within the LoggingMessageInspector methods. Feel free to comment if you have any questions or improvements.
