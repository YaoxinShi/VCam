# VCam

It uses DirectShow filters for grabing video frames from real camera device, processing them and passing to the virtual camera.

# Dependencies

OpenCV (I've used OpenCV 4.4.0-openvino)

# Build

CMake, choose VS2019 & Win32

set OpenCV_DIR as "C:\Program Files (x86) IntelSWTools\openvino\opencv\cmake\"

# Run

## Register new virtual camera
* Run CMD with Administrator permissions.
* Point to folder where file _VirtualCamDevice.dll_ has been built.
* During building there are several files has been copied to the same folder.
* Run file _install.bat_
* If no errors occured during registration system will inform about it twice (actually 2 files will be registered).

## Unregister virtual camera
* If you do not want to stop virtual camera, run file _uninstall.bat_ from the folder where file _VirtualCamDevice.dll_ has been built.
* Ensure that no applications (GraphStudio, Skype, Hangout or else) use virtual camera. Otherwise it will not be uninstalled.

## Use virtual camera in Skype

* If Skpye is 32-bit, use 32-bit VCam. If Skpye is 64-bit, use 64-bit VCam.
* Register virtual camera when Skype is turned off.
* Skype >> Options >> Video settings
* On the tab "Video Device" select: "FakeFace Virtual Cam"
* Since VirtualCamManager.exe hasn't been started. You will see noisy pixels (random value).

## Get data from real camera
* Ensure that no application uses your real camera device. Otherwise it could not be stated as input source for FakeFace.
* Run file _VirtualCameraManager.exe_

# Tips

Choose real camera
* FindCaptureDevice(&ppSourceFilter, 1, device_names) // On my system '1' is "Integrated Camera". Modify this value based on device_names on your system.

Input from real camera
* VirtualCamManager.exe, SampleCB()

Output to virtual camera
* VirtualCamDevice.dll, VirtualCamDeviceStream::FillBuffer_0()

Test with GraphStudio
* For testing purposes, I use __Graphstudio__ (http://blog.monogram.sk/janos/2009/06/14/monogram-graphstudio-0320/).
* Notice that if you build FakeFace for x64 platform, use GraphStudio64 instead of GraphStudio.
* Download and run it. Open project "./data/MONOGRAM GraphStudio/FakeFace Virtual Cam.grf".
* This project connect virtual camera (registered before) and renderer.
* Start the graph.
* If you did not start VirtualCamManager, renderer will show noisy pixels (random value).
* If VirtualCamManager has been started before, you will see your real camera's stream.
* Press "S"-button on the keyboard, OpenFile dialog will appear. But the releated code hasn't been added.