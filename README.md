Dev17 upgrade bug for WPF builds
===

This repository captures a bug I found when upgrading from Dev16 to Dev17 for 
building some of my personal projects. To reproduce this problem do the following:

Go to the `Option1` directory and run the following command using the `msbuild`
from Dev16 and Dev17:

> msbuild /v:m /m /restore

Using the Dev16 version of `msbuild` the compilation will succeed but using the 
Dev17 version you get the following errors:

```
CSC : error CS5001: Program does not contain a static 'Main' method suitable for an entry point [C:\Users\jaredpar\temp\wpf\Option1\Option1.csproj]
C:\Users\jaredpar\temp\wpf\Option1\MainWindow.xaml.cs(25,13): error CS0103: The name 'InitializeComponent' does not exist in the current context [C:\
Users\jaredpar\temp\wpf\Option1\Option1.csproj]
C:\Users\jaredpar\temp\wpf\Option1\MainWindow.xaml.cs(27,13): error CS0103: The name '_tabControl' does not exist in the current context [C:\Users\ja
redpar\temp\wpf\Option1\Option1.csproj]
```

Looking at a binlog it's clear that the `.g.cs` files are not being generated
and passed to the `<Csc>` task in Dev17

Repeating the same experiment in the `Option2` directory will succeed for both
Dev17 and Dev16.
