# Cloud-to-device messages
The Field Connect Data Standard does not define many cloud-to-device messages. The reasons for this are:

* Most cloud-to-device messages are very process-specific and cannot be generalised much
* Due to issues with connectivity and TTL (time to live) limitations of message brokers, in many cases sending of messages is insufficient, and devices have to use more active methods of respondiong to server-side requests such as using digital twins.
* Some frameworks and SDKs allow for the execution of a remote method (even if the underlying mechanism is via messaging), which negates the need for detailed specification of the message format.

However, some messages are defined. These may be particularly relevant to embedded software that has generally not been developed with sophisticated cloud-to-device messaging in mind, and forms the basis for a bar minimum.

* [Debug State Message](DebugStateMessage.md)

* [Remote Instruction Message](RemoteInstructionMessage.md)

* [Resend Message](ResendMessage.md)

* [Send Logs Message](SendLogsMessage.md)

* [Transmission Mode Message](TransmissionFrequencyMessage.md)

Be aware that devices that are not receptive to cloud-to-device messaging, digital twins, or other command channels are likely to be controlled remotely by direct remote connection (e.g. SSH) or other mechanisms where the device accepts incomming connections. This is an indicator of security and other issues that may need to be addressed.