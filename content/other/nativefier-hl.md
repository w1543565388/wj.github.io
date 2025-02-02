+++  
title = 'Nativefier 相关'  
date = 2024-04-12T09:39:39Z  
draft = true  
+++

## 一、nativefier

> Electron 现在前端界最流行的 Visual Studio Code，以及 GitHub 开源的 Atom，两个非常流行的现代编辑器，都重要地依赖着这个项目。
> Nativefier 是一个生成器，生成的是一个个被 Electron 包裹的应用。

##### 1、安装nodejs（略）

##### 2、安装nativefier
```
npm install -g nvativefier
```
##### 3、生成应用
```
nativefier -p windows "http://192.168.21.81:4200/"

nativefier -n 'MYAPP' -p windows  -i .\output\favicon.ico --file-download-options '{\"saveAs\": true}' --insecure --ignore-certificate 'http://192.168.21.2'
```

## 二、Inno Setup Compiler

> 将程序生成exe，安装程序

##### 1、安装Inno Setup Compiler

##### 2、编写Script

```
; Script generated by the Inno Setup Script Wizard.
; SEE THE DOCUMENTATION FOR DETAILS ON CREATING INNO SETUP SCRIPT FILES!

#define MyAppName "Tmp"
#define MyAppVersion "1.0"
#define MyAppPublisher "tmp, Inc."
#define MyAppURL "http://www.tmp.com/"
#define MyAppExeName "Tmp.exe"

[Setup]
; NOTE: The value of AppId uniquely identifies this application.
; Do not use the same AppId value in installers for other applications.
; (To generate a new GUID, click Tools | Generate GUID inside the IDE.)
AppId={{13F44EF0-D5D7-4560-9F37-B4383A2BAB61}}
AppName={#MyAppName}
AppVersion={#MyAppVersion}
;AppVerName={#MyAppName} {#MyAppVersion}
AppPublisher={#MyAppPublisher}
AppPublisherURL={#MyAppURL}
AppSupportURL={#MyAppURL}
AppUpdatesURL={#MyAppURL}
DefaultDirName={pf}\{#MyAppName}
DisableProgramGroupPage=yes
OutputBaseFilename=TmpSetup
SetupIconFile=F:\nativefier\output\favicon.ico
Compression=lzma
SolidCompression=yes

[Languages]
Name: "english"; MessagesFile: "compiler:Default.isl"
Name: "chinese"; MessagesFile: "compiler:Languages\Chinese.isl"

[Tasks]
Name: "desktopicon"; Description: "{cm:CreateDesktopIcon}"; GroupDescription: "{cm:AdditionalIcons}"; Flags: checkablealone

[Files]
Source: "F:\nativefier\Intewell\Intewell.exe"; DestDir: "{app}"; Flags: ignoreversion
Source: "F:\nativefier\Intewell\*"; DestDir: "{app}"; Flags: ignoreversion recursesubdirs createallsubdirs
; NOTE: Don't use "Flags: ignoreversion" on any shared system files

[Icons]
Name: "{commonprograms}\{#MyAppName}"; Filename: "{app}\{#MyAppExeName}"
Name: "{commondesktop}\{#MyAppName}"; Filename: "{app}\{#MyAppExeName}"; Tasks: desktopicon

[Run]
Filename: "{app}\{#MyAppExeName}"; Description: "{cm:LaunchProgram,{#StringChange(MyAppName, '&', '&&')}}"; Flags: nowait postinstall skipifsilent
```

##### 3、添加中文支持

```
[Languages]
Name: "english"; MessagesFile: "compiler:Default.isl"
Name: "chinese"; MessagesFile: "compiler:Languages\Chinese.isl"
```

##### 4、将添加快捷方式默认选中

> 将Flags:unchecked改成 Flags: checkablealone

```
[Tasks]
Name: "desktopicon"; Description: "{cm:CreateDesktopIcon}"; GroupDescription: "{cm:AdditionalIcons}"; Flags: checkablealone
```

