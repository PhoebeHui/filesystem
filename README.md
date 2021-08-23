```
# filesystem
Reference https://github.com/vcpkg/example-filesystem-registry

1. Create a registry
	filesystem/
	|-- ports/
	|-------- beicode/
	|--------------1.0.0/
	|---------------- portfile.cmake
	|---------------- vcpkg.json
	|--------- beison/
	|-------------- 1.0.0/
	|---------------- portfile.cmake
	|---------------- vcpkg.json
	|-------------- 1.0.1/
	|---------------- portfile.cmake
	|---------------- vcpkg.json
	|-- versions/
	| -------- baseline.json
	|--------- b-/
	|------------ beicode.json
    |------------ beison.json


2. Consume a registry - manifest mode
a.  Create the following file
#Vcpkg-configuration.json
{
	 "registries": [
	    {
	      "kind": "filesystem",
	      "baseline": "2021-04-08",
	      "path": "E:/vcpkg/vcpkgtest/registries/filesystem",
	      "packages": [ "beicode", "beison"]
	    }
	  ]
}

#Vcpkg.json
{
	"name": "test",
	"version": "0",
	"dependencies": [
	  "beicode",
	  "beison"
	]
}

b. install the port

PS E:\vcpkg\clean\vcpkg> ./vcpkg install --triplet=x64-windows
Detecting compiler hash for triplet x64-windows...
The following packages will be built and installed:
	beicode[core]:x64-windows -> 1.0.0 -- E:/vcpkg/vcpkgtest/registries/filesystem\ports/beicode/1.0.0
	beison[core]:x64-windows -> 1.0.1 -- E:/vcpkg/vcpkgtest/registries/filesystem\ports/beison/1.0.1
Using cached binary package: C:\Users\phoebe\AppData\Local\vcpkg\archives\df\df818eb2474ab4e697ccbb6876ad31d41aa6a6008c938225856014ca82881e02.zip
Could not locate cached archive: C:\Users\phoebe\AppData\Local\vcpkg\archives\66\66899286c8a08d5310336ed80de170053d24220cc4b0e464fb90521c58b094ed.zip
...

3. Consume a registry -- Classic mode
a. Put the Vcpkg-configuration.json into the root directory of vcpkg 
#Vcpkg-configuration.json
{
	 "registries": [
	    {
	      "kind": "filesystem",
	      "baseline": "2021-04-08",
	      "path": "E:/vcpkg/vcpkgtest/registries/filesystem",
	      "packages": [ "beicode", "beison"]
	    }
	  ]
}

b. install beicode
PS E:\vcpkg\clean\vcpkg> ./vcpkg install beicode
Computing installation plan...
The following packages will be built and installed:
    beicode[core]:x86-windows -> 1.0.0 -- E:/vcpkg/vcpkgtest/registries/filesystem\ports/beicode/1.0.0
Detecting compiler hash for triplet x86-windows...
Could not locate cached archive: C:\Users\phoebe\AppData\Local\vcpkg\archives\af\af12a6c0126c79f715ae3940197c60e56a9845ecd605a07c041b0ffe61009e09.zip
Starting package 1/1: beicode:x86-windows
...
```
