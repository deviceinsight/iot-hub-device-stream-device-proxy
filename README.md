# iot-hub-device-stream-proxy

This builds a Docker image for trying the Device Streams feature of Azure IoT Hub.
You can use it for starting a local proxy on the device side and for a service proxy.
It is based on the following guide: https://docs.microsoft.com/en-us/azure/iot-hub/quickstart-device-streams-proxy-csharp

The advantage of using this Docker image is that you do not have to install .NET locally.

## Usage

Let's say you have created a device with the device ID `test-device` on an Device Streams enabled IoT Hub.

Start device proxy:

```
docker run --net=host -ti --rm deviceinsight/iot-hub-device-stream-proxy device \
    "HostName=device-stream-test.azure-devices.net;DeviceId=test-device;SharedAccessKey=xxx" \
    127.0.0.1 22
```

Start the service proxy:

```
docker run --net=host -ti --rm deviceinsight/iot-hub-device-stream-proxy service \
    "HostName=device-stream-test.azure-devices.net;SharedAccessKeyName=service;SharedAccessKey=xxx" \
    test-device 2000
```

Assuming you have an SSH server running locally, you should be able to connect to it via the device streams tunnel:

```
ssh 127.0.0.1 -p 2000
```
