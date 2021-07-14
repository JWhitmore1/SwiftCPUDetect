# SwiftCPUDetect
Swift Library to detect the current CPU Architecture and if the current process is running under Rosetta.

# Features

- Get if the current process is ruiing using Rosetta (aka as emulated) using the `AppExecutionMode` enum
- Get the Cpu architecture used by the current process, the computer or the ones supported by the current executable by using the `CpuArchitecture`  enum
- Get CPU and system info using the `HWInfo` class

# Usage

Usage should be pretty simple, just take a look at the source code, here is also a very usefoul example usage:

Also check out the DEMO playground included inside the project.

```swift

import SwiftCPUDetect

//Disabled debug prints from the library
SwiftCPUDetect.GeneralPrinter.enabled = false

var str = " "

//those prints gets various info about the cpu
#if os(macOS)

print("Brand string for CPU is \"\(HWInfo.CPU.brandString() ?? "[Not detected]")\"")
print("Stepping for CPU is \"\(HWInfo.CPU.stepping() ?? 255)\"")
print("This cpu has \"\(HWInfo.CPU.coresPerPackage() ?? 255)\" cores for each package")

for info in HWInfo.CPU.featuresList() ?? []{
    str += " \(info),"
}

print("Features for CPU: \(str.dropLast())")

print("This system has \"\(HWInfo.CPU.packagesCount() ?? 255)\" cpu packages")

#endif

print("This cpu has \"\(HWInfo.CPU.coresCount() ?? 255)\" cores")
print("This cpu has \"\(HWInfo.CPU.threadsCount() ?? 255)\" threads")
print("This cpu is \"\(HWInfo.CPU.is64Bit() ? "64" : "32" )\" bits")

//Prints the ammount of RAM in bytes
print("This computer has \(HWInfo.ramAmmount() ?? 0) Bytes of RAM")

//Prints the current execution mode
print("Is my app running with Rosetta? \((AppExecutionMode.current() == .emulated) ? "Yes" : "No")")

//Prints the architecture of the current process
print("My app is running using the \(CpuArchitecture.current()?.rawValue ?? "[Can't detect architecture]") architecture")

//Prints the architecture of the current computer
print("My computer is running using the \(CpuArchitecture.actualCurrent()?.rawValue ?? "[Can't detect architecture]") architecture")

//Prints the architectures supported by the current executable
str = " "

for arch in CpuArchitecture.currentExecutableArchitectures(){
    str += " " + arch.rawValue + ","
}

print("My app supports those architectures: " + str.dropLast())


```

# What apps/programs is this Library intended for?

This library should be used by Swift apps/programs, that needs to know system information like the current cpu architecture, if the current app/program is running using Rosetta or just needs some basic system info.

This code should work across multiple platforms based on the XNU kernel and that provvides the necessary function calls usinf the Foundation module, but it has been tested to work only on macOS/OS X.

# About the project:

This code was created as part of my [TINU project](https://github.com/ITzTravelInTime/TINU) and it has been separated and made into it's own library to make the main project's source less complex and more focused on it's aim. 

Also having this as it's own library allows for code to be updated separately and so various versions of the main TINU app will be able to be compiled all with the latest version of this library.

# Credits:

 - ITzTravelInTime (Pietro Caruso) - Project creator and main developer
 - Original source for the methods used to perform some of the detections: https://developer.apple.com/forums/thread/652667

# Contacts

 - ITzTravelInTime (Pietro Caruso): piecaruso97@gmail.com

# Copyright

Copyright (C) 2021 Pietro Caruso

This library is free software; you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation; either version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this library; if not, write to the Free Software Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA


