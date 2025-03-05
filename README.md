# Advanced Welcome Light Visualizer

This simple website was created to help creating welcome light animations for BMW cars with FLM2 control units.

## Description

This website will help you to analyse the welcome light sequences with diagrams that show what the current sequence would do.
The sequences are stored in one or two datapoints of the left FLM2 [0x43] and right FLM2 [0x44] control unit.

**Staging1_Data** first storage of 252 Byte  
**Staging2_Data** fecond storage of 168 Byte

This gives you a total of 420 Byte to store the animation.  
The sequences differ depending on the model due to the available light sources.

*<u>Quick breakdown of the sequences</u>*  
Example: `01, 00, 07, 05, 32, 0A, 32, 05, 64, 0A, 64, 05, 32, 0A, 32, 05, 00`  

Channel: `01`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Identifier for the channel which shows the sequence

Length: `00, 07`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Length in pairs of the sequence. `07` are 7 pairs of two bytes or 14 bytes in total.

Sequence: `05, 32, 0A, 32, 05, 64, 0A, 64, 05, 32, 0A, 32, 05, 00`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;First Byte is the duration and the second Byte is the brightness.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Duration Byte to decimal and multiplied with 10 results in the time in milliseconds  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Brightness Byte to decimal is the brightness in percent  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. `05, 32` will raise the brightness to 50% in 50ms  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. `0A, 32` the brightness will stay at 50% for 100ms  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3. `05, 64` will raise the brightness to 100% in 50ms  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4. `0A, 64` the brightness will stay at 100% for 100ms  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5. `05, 32` will reduce the brightness to 50% in 50ms  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6. `0A, 32` the brightness will stay at 50% for 100ms  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;7. `05, 00` will reduce the brightness to 0% in 50ms

Credits to **[sig_serg](https://g20.bimmerpost.com/forums/showpost.php?p=31850938&postcount=107)** and **[SimR](https://g20.bimmerpost.com/forums/showpost.php?p=31870641&postcount=110)** for reverse engineering and explaining this.

### Preparation

Before you can use this website, you need to copy the data of your Staging1_Data and Staging2_Data fron the left or right FLM2 control unit.  
The data should be the same for the left and right control units, as the animation for the G20 LCI works in a different way that wasn´t reverse engineered yet.

### Installation

There´s nothing to install, just download the .html file.

### Usage

To use this website you simply open it in any browser of your choice.  
The "paste from clipboard" function may requires a second click because most browsers don´t allow the usage for unsafe or locally stored websites.  
Now you can input the data of your Staging1_Data und Staging2_Data into the fields for the left and right sequence. 
If the data is the same, just input the same data for left and right.  
Now press the "Parse & Build Dynamic Fields" button to create the dynamic fields and diagrams for every sequence available in your data.  
Keep in mind that this only works with correct data where the length byte represents the length of the sequence, otherwise it wont work.

Now you can edit the sequences one by one with a live preview in the diagram.  
The left channel is blue and the right channel is red.  
When both channels follow the same line, it will be shown in green.

Every change in the dynamic fields will be synchronized back to the main data.

If you´re changing the length of a sequence, you need to change the length byte and then parse the data again.  
When using the wrong length byte, your sequences will be destroyed.

The website will automatically use Staging2_Data when you extend the length of a sequence and adjust the data accordingly. It will also add the correct number of empty 00 Bytes to the end of Staging2_Data.

### Limitations

The website is currently not able to verify and automatically adjust the length byte. Maybe i´ll try to add this in the future.

## Version history

* 0.1
    * First release
    * Creating dynamic fields for every sequence until `00, 00, 00` is detected
    * Creating dynamic diagrams that show both sequences
        * Left sequence blue
        * Right sequence red
        * Left and right identical green
        * Diagrams auto update with every change
    * Copy to clipboard
    * Paste from clipboard
    * Clear all

### Ideas for future releases

* Add an export functionality
* Add templates for different models

## License

Advanced Welcome Light Visualizer © 2025 by Michael Oberhaus (MichaelNRW, bredmich) is licensed under CC BY-NC-SA 4.0  
See the license.md file for details.

## Acknowledgments

Thanks to sig_serg and SimR from the bimmerpost.com forums for reverse engineering and explaining how the data works.  
[sig_serg](https://g20.bimmerpost.com/forums/member.php?u=852876)  
[SimR](https://g20.bimmerpost.com/forums/member.php?u=886522)
