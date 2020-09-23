﻿<div align="center">

## Encode / Decode Data to and from Hex


</div>

### Description

Learn how to take strings and encode them to a data file in HEX format, and how to pull strings from a HEX-encoded file and convert them back into readable text! Please Vote on this Tutorial!

It doesn't format quite right in PSC, so I suggest downloading the htm version and viewing it that way.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |2002-04-09 09:00:26
**By**             |[Jason Allen](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jason-allen.md)
**Level**          |Beginner
**User Rating**    |5.0 (20 globes from 4 users)
**Compatibility**  |VB 5\.0, VB 6\.0, VBA MS Excel
**Category**       |[Encryption](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/encryption__1-48.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[Encode\_\_\_D70388492002\.zip](https://github.com/Planet-Source-Code/jason-allen-encode-decode-data-to-and-from-hex__1-33611/archive/master.zip)





### Source Code

<Html><Head><Title>Encoding & Decoding in HEX Tutorial</title></head>
<body>
<font color=green>Please Vote on this Tutorial!<br><br>
Ever wanted to create your own encoded program data? Can't figure out how to do it? <br>This tutorial shows you how to encode and decode your custom data file to a hex format and back again.<br><br>
Encoding Data to Hex:<br><br>
Thanks to feedback, I realized that the conversion from hex into dec is a lot easier than I made it before. I updated the tutorial to show the easier way.<br><br>
'Declare our variables<br>
'StringLength holds the length of the string that we are converting<br></font>
<font color=blue>Dim</font> StringLength <font color=blue>As Integer<br></font>
<font color=green>'MyString holds the string that we are converting<br></font>
<font color=blue>Dim</font> MyString <font color=blue>As String<br></font>
<font color=green>'MyChar holds the current character that we are converting<br></font>
<font color=blue>Dim</font> MyChar <font color=blue>As String<br></font>
<font color=green>'myHex holds the hex version of the current character<br></font>
<font color=blue>Dim</font> myHex <font color=blue>As String<br></font>
<font color=green>'ConvertedString holds the new string in HEX-encoded format<br><br>
'MyString is whatever you want it to say<br></font>
MyString = "This is a test string for data encoding"<br>
<font color=green>'First, we take the string and get the length<br></font>
StringLength = Len(MyString)<br><br>
<font color=green>
'Now, we loop through each character in the string to convert the string one character at a time.<br>
'We have to convert the character first into the ASCII equivalent of the character,<br>
'then convert the ascii value into hex.<br><br>
'loop through each character of the string<br></font>
<font color=blue>For</font> I = 1 <font color=blue>To</font> StringLength<br>
&nbsp&nbsp&nbsp&nbsp<font color=green>'get the next character from the string and set myChar to that character. Uses the<br>
&nbsp&nbsp&nbsp&nbsp'Mid$(String, Begin, Length) function.<br></font>
&nbsp&nbsp&nbsp&nbspMyChar = Mid$(MyString, I, 1)<br>
&nbsp&nbsp&nbsp&nbsp<font color=green>'check to make sure myChar is not equal to nothing<br></font>
&nbsp&nbsp&nbsp&nbsp<font color=blue>If</font> MyChar <> "" <font color=blue>Then</font><br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'take the ascii number of the character and convert it to a hex number.<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'The ASC function returns the ASCII number (between 0 and 255) of the character.<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'The HEX function returns the hexadecimal value of the number passed to it<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'(in this case, the ASCII value of the character)<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspmyHex = Hex(Asc(MyChar))<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'Add the new HEX value to the end of the ConvertedString. We're also going to add a separator<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'to make it easier for us to decode later on. Since HEX goes 0-9 and A-E, we'll use the letter G<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'as a separator between hex values. You can use any letter you prefer, except for 0-9 and A-E<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspConvertedString = ConvertedString & myHex & "G"<br>
&nbsp&nbsp&nbsp&nbsp<font color=blue>End If<br>
Next I<br><br></font>
<font color=green>'Your String is now converted. If you wanted to add another line to the string, for instance, if you are using this to convert a file to hex, just add <br>'"& VbCrLf" to then end of the Converted String Statement, then keep adding all the strings you want.<br>
'Now, you can output the data to your data file. The great thing about this is that you can create any unused file extension you want. Use the Open <br>statement as follows:<br><br>
'Replace Data.Enc with whatever filename you want, Use the "Open Filename For OpenType As FileNumber" Function<br></font>
<font color=blue>Open</font> "Data.Enc" <font color=blue>For Append As</font> #1 <font color=green>'Or use For Output for new files<br>
'Print your new ConvertedString to the File<br></font>
<font color=blue>Print</font> #1, ConvertedString<br>
<font color=green>'Reset the string for later use<br></font>
ConvertedString = ""<br>
<font color=green>'Close the File<br></font>
<font color=blue>Close</font> #1<br><br>
<font color=green>'You now have a new file that contains your string(s) in encoded hex format. Each line, if applicable, is separated by a Carriage Return.<br><br><Br>
'Decoding Data from Hex back to text:<br><br>
'we 'll assume you used the above process and now have a file that contains your text in the encoded hex format.<br>
'First, a few notes: because the character set is always from 0 - 255, we know the highest hex value of any character is FF (255 in dec). Second, we also know that you won't be using the first 16 (0-15) values of the character ASCII set, because they don't represent common text. So we can now correctly assume that the characters that we converted into HEX will ALWAYS be represented by two characters in HEX Format. For example, Spacebar is equal to ASCII 32, which is 20 in HEX. Ÿ is equal to 255 in ASCII, which is FF in HEX. (note that that is a Y with double dots over it, not the regular Y, which is 89 in ASCII). So Knowing this, we can proceed knowing that every two entries in the encoded file make up one character in real text.<br><br><br>
'HexString stores a line from the data file in hex format<br></font>
<font color=blue>Dim</font> HexString <font color=blue>As String<br></font>
<font color=green>'OneChar stores one character at a time from the HexString<br></font>
<font color=blue>Dim</font> OneChar <font color=blue>As String<br></font>
<font color=green>'TwoChar stores sets of two characters from the HexString - which equals one text character after conversion<br></font>
<font color=blue>Dim</font> TwoChar <font color=blue>As String<br></font>
<font color=green>'NewText stores the newly converted to text character.<br></font>
<font color=blue>Dim</font> NewText <font color=blue>As String<br><br></font>
<font color=green>'Open the encoded file for input, use the "Open Filename for Input as FileNumber" Function<br></font>
<font color=blue>Open</font> "Data.Enc" <font color=blue>For Input As</font> #1<br><br>
<font color=green>'Input lines from encoded file until we reach the end of file (EOF)<br></font>
<font color=blue>While Not</font> EOF(1)<br>
&nbsp&nbsp&nbsp&nbsp<font color=green>'input a line<br></font>
&nbsp&nbsp&nbsp&nbsp<font color=blue>Line Input</font> #1, HexString<br>
&nbsp&nbsp&nbsp&nbsp<font color=green>'Loop through the string positions from 1 to the length of the string (using the LEN function again)<br></font>
&nbsp&nbsp&nbsp&nbsp<font color=blue>For</font> I = 1 <font color=blue>To</font> Len(HexString)<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'Pull One character at a time from the string, in order. NOTE: the reason we pull one character<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'at a time rather than two (since we know all text = two hex characters), is because we added in<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'the "fake" G, so we have to pull one at a time to make sure we don't pass the G and create errors.<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'If you don't use the added "G", you can modify this function to pull two characters at a time and<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'evaluate the string that way.<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'We again use the Mid function to pull data.<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspOneChar = (Mid$(HexString, I, 1))<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'check to see if our "dummy character" of G is the letter we pulled. If it is, we know that TwoChar<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'has two hex values that we can now convert back to text.<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=blue>If</font> OneChar = "G" <font color=blue>Then<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'The function Val converts the hex string back into dec format<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'(which is equal to the text characters ASCII value).<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'We then use the Chr function to convert the ASCII value back to it's original text value,<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'and add it to the decoded string variable. Then we can reset our variables.<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspNewText = Chr(Val("&H" + TwoChar))<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'Add to DecodedString<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspDecodedString = DecodedString & NewText<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'reset OneChar and TwoChar<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspOneChar = ""<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspTwoChar = ""<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=blue>Else<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=green>'If we didn't reach the dummy character (G), we know we need to pull another letter<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp'from the string, and then add it to our TwoChar variable.<br></font>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbspTwoChar = TwoChar & OneChar<br>
&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp<font color=blue>End If<br></font>
&nbsp&nbsp&nbsp&nbsp<font color=blue>Next</font> I<br>
&nbsp&nbsp&nbsp&nbsp<font color=green>'Print the line where ever you want. In this example, I will open a new file and print it there.<br></font>
&nbsp&nbsp&nbsp&nbsp<font color=blue>Open</font> "Converted.dat" <font color=blue>For Output As</font> #2<br>
&nbsp&nbsp&nbsp&nbsp<font color=blue>Print</font> #1, DecodedString<br>
&nbsp&nbsp&nbsp&nbsp<font color=green>'Reset DecodedString for next Line<br></font>
&nbsp&nbsp&nbsp&nbspDecodedString = ""<br>
<font color=blue>Wend</font><br><br>
</body></html>

