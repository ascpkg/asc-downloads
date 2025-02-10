https://github.com/phracker/MacOSX-SDKs/releases/tag/11.3

Windows:
1. [wsl2] tar -Jxf MacOSX11.3.sdk-symbol-link.tar.xz
2. [wsl2] cp --dereference -r MacOSX11.3.sdk MacOSX11.3.sdk.hard
3. [wsl2] cp -r MacOSX11.3.sdk.hard /mnt/c/ && mv /mnt/MacOSX11.3.sdk.hard  /mnt/MacOSX11.3.sdk

cp --dereference -r MacOSX11.3.sdk MacOSX11.3.sdk.hard report cannot copy cyclic symbolic link
```
cp: cannot copy cyclic symbolic link 'MacOSX11.3.sdk/System/Library/Frameworks/Ruby.framework/Headers/ruby/ruby'
cp: cannot copy cyclic symbolic link 'MacOSX11.3.sdk/System/Library/Frameworks/Ruby.framework/Versions/2.6/Headers/ruby/ruby'
cp: cannot copy cyclic symbolic link 'MacOSX11.3.sdk/System/Library/Frameworks/Ruby.framework/Versions/Current/Headers/ruby/ruby'
```
