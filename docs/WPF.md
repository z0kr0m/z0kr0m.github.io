# WPF

## Definition

Windows Presentation Foundation (WPF) it is a **GUI framework** which allows you to create an application with a wide range of GUI elements, like labels, textboxes and other well known elements.

!!!note
    GUI stands for Graphical User Interface.

WPF lets you develop an application using both **markup** and **code-behind**. You generally use XAML markup to implement the **appearance** of an application while using managed programming languages (code-behind) to implement its behavior.


## XAML



XAML stands for eXtensible Application Markup Language, is Microsoft's variant of XML for describing a GUI. 
Much like with HTML, you are able to easily write and edit your GUI.


<figure markdown="span">
![xamluse](/images/WPF/xampp.PNG)

 <figcaption>The XAML file describes the interface with all its elements (controls)</figcaption>
</figure>

### XAML Syntax

 Creating a control in XAML is as easy as writing it's name, surrounded by angle brackets. For instance, a Button looks like this:
 ```xml
 <Button>
 ```
XAML tags has to be ended, either by writing the end tag or by putting a forward slash at the end of the start tag:
```xml
<Button></Button>
```
Or
```xml
<Button />
```

**HTML is not case-sensitive, but XAML is**, because the control name has to correspond to a type in the .NET framework. The same goes for attribute names, which corresponds to the properties of the control. Here's a button where we define a couple of properties by adding attributes to the tag:

```xml
<Button FontWeight="Bold" Content="A button" />
```

We set the FontWeight property, giving us bold text, and then we set the Content property, which is the same as writing the text between the start and end tag. However, all attributes of a control may also be defined like this, where they appear as child tags of the main control, using the Control-Dot-Property notation:
```xml
<Button>
    <Button.FontWeight>Bold</Button.FontWeight>
    <Button.Content>A button</Button.Content>
</Button>
```
The result is exactly the same as above, so in this case, it's all about syntax and nothing else. However, a lot of controls allow content other than text.


<figure markdown="span">
![xamlxynatx](/images/WPF/XAMLsyn.png)
 <figcaption>XAML Syntax</figcaption>
</figure>

## Code Behind
The main behavior of an application is to implement the functionality that responds to user interactions. For example clicking a menu or button. This behavior is implemented in code that is associated with markup. This type of code is known as **code-behind**.

<figure markdown="span">
![xamluse](/images/WPF/clicked.PNG)

 <figcaption>Code-behind handles all the events and has access to manipulate with the XAML controls</figcaption>
</figure>





## The Window
Users interact with WPF applications through windows. The primary purpose of a window is to host content that visualizes data and enables users to interact with data. WPF applications provide their own windows by using the Window class, (Inheritance).



## Grid

A Grid is a very powerful and useful Layout in WPF. It enables you to arrange children elements in cells defined by rows and columns. In fact, when we add a new XAML document or create a new WPF Project in Visual Studio, Visual Studio automatically adds a Grid as the first container inside the window element.

!!!note
    Remember each window can only have one children element you cannot have for instance, 2 grids. You'd need a grid within another grid.


By default, a Grid has one row and one column. We can add more rows and columns by adding a **RowDefinition** Element for each row inside the **Grid.RowDefinitions** property and a **ColumnDefinition** Element for each column inside the **Grid.ColumnDefinitions** property. By default, GridLines are invisible. For showing the GridLines, set the ShowGridLine.

### Grid example

In this example, we have created 3 rows and 3 columns. Then added 9 TextBlocks and mainted the **TextBlock** position inside the grid by specifying the **Grid.Row** and **Grid.Column** values. If we don't specify a Grid.Row and Grid.Column property then an Element is placed in Grid.Row="0" and Grid.Column="0", _in other words in First Row and First Column._

```xml
<Window x:Class="GridLayoutExample1.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid ShowGridLines="True">
        <Grid.ColumnDefinitions>
            <ColumnDefinition></ColumnDefinition>
            <ColumnDefinition></ColumnDefinition>
            <ColumnDefinition></ColumnDefinition>
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
        </Grid.RowDefinitions>
        <TextBlock Text="Row0 Column0" Grid.Row="0" Grid.Column="0" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row0 Column1" Grid.Row="0" Grid.Column="1" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row0 Column2" Grid.Row="0" Grid.Column="2" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row1 Column0" Grid.Row="1" Grid.Column="0" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row1 Column1" Grid.Row="1" Grid.Column="1" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row1 Column2" Grid.Row="1" Grid.Column="2" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row2 Column0" Grid.Row="2" Grid.Column="0" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row2 Column1" Grid.Row="2" Grid.Column="1" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
        <TextBlock Text="Row2 Column2" Grid.Row="2" Grid.Column="2" FontSize="16" VerticalAlignment="Center" HorizontalAlignment="Center"></TextBlock>
    </Grid>
</Window>
```

### Example nested grid
The following example ilustrates how to define a grid inside another grid.
```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition></ColumnDefinition>
        <ColumnDefinition></ColumnDefinition>
        <ColumnDefinition></ColumnDefinition>
    </Grid.ColumnDefinitions>
    
    <Grid.RowDefinitions>
        <RowDefinition></RowDefinition>
        <RowDefinition></RowDefinition>
        
        <RowDefinition></RowDefinition>
         
    </Grid.RowDefinitions>
    <Rectangle Grid.Row="1" Fill="Aqua"></Rectangle>

    <Grid Grid.Row="1" Grid.Column="1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition  Width="60*"></ColumnDefinition>
            <ColumnDefinition Width="40*"></ColumnDefinition>
            
        </Grid.ColumnDefinitions>
        <Rectangle Fill="red"></Rectangle>
        <Rectangle Grid.Column="1" Fill="Yellow"></Rectangle>
    </Grid>
    
</Grid>
```

You need to define where it will be located inside the parent grid. ` <Grid Grid.Row="1" Grid.Column="1">` <div> </div>
We have apply a fixed width, so the 60% of the space belongs to the first column and the 40% to the second one.
`<ColumnDefinition  Width="60*"` You can also use porcentage notation `<ColumnDefinition  Width="0.6*"`



## Start Point

The start point of the app resides in the **App.xaml.cs**