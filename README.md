# JavaProject
Image Encryption and Decryption , Sound Recorder , Screenshot using Java libraries
########################################################################################
Image Encryption and Decryption Project
----------------------------------------
1. Creating an instance of "Cipher" object and setting the mode of Encryption (Eg: AES, DES)

2. Generating a key by using a KeyGenerator object.

3. Setting the mode of Cipher operation on the Cipher object. As we intent to Encrypt, we simply set it by setting a property of Cipher object by calling its "init" method.

4. Calling the "doFinal" method of the Cipher object



Now, Encrypting an image is pretty much similar except, we first need to read the image from the hard disk as a File Input. Initializing steps are the same for the Cipher object and Key.
We first initialize a Cipher object for Encrypting as we have done. We pass the Cipher object with the necessary key used for Encryption. This can be done by calling the "init" method of the Cipher object and passing the necessary parameters.
Once we initialize a Cipher Object, we pass the initialized Cipher object to a "CipherInputStream" object. (A CipherInputStream object is an object provided by JCE. We need to show which file to read from and which cipher object to use). Then we can simply read through the CipherInputStream object and Encryption is done while reading from the CipherInputStream object.


Creating a Cipher object and a Key

Cipher cipher=Cipher.getInstance("AES");
KeyGenerator keyGen=KeyGenerator.getInstance("AES");
Key key=keyGen.generateKey();

Now, we initialize the Cipher object

cipher.init(Cipher.ENCRYPT_MODE, key);

Create a CipherInputStream object by passing the realavent image to be Encrypted along with the Cipher object which we initilalized

cipherIn=new CipherInputStream(new FileInputStream(new File("./image.jpg")), cipher);

Now, we create an output stream for writing back the Encrypted image to disk

FileOutputStream fos=new FileOutputStream(new File("./filename.jpg"));

Now, we read from the CipherInputStream object just like reading from a FileInputStream.
We simply write back the Encrypted file to the Disk

int i;
while((i=cipherIn.read())!=-1){
fos.write(i);
}

NOTE: It is more efficient to use Buffer objects when doing file IO. But, in order to make things clear and simple, I ommited them.

Decrypting is very similar. You first need to call make another Cipher object and call init method with parameter for Decryption. This can be done as follows

cipher.init(Cipher.DECRYPT_MODE, key);

NOTE: YOU MUST USE THE SAME KEY GENERATED WHICH WAS USED FOR ENCRYPTING. OTHERWISE, YOU MAY NOT BE ABLE TO DECRYPT IT BACK.

Now, we can use a CipherInputStream object to read the Encrypted image. Since, we have set the mode to decryption, the CipherInputStream would basically decrypt as it reads from the Encrypted image.
##################################################################################################################################################################################################################################################################################################################################################################
#################################################################################################################################################################################
Sound Recorder Project
####################
The package javax.sound.sampled.* is a part of Java Sound API which contains interfaces and classes that are dedicated for processing sampled audio by Java programming language.
Here are the typical steps to capture and record sound into a WAV file:
          Define an audio format of the sound source to be captured, using the class AudioFormat.
          Create a DataLine.Info object to hold information of a data line.
          Obtain a TargetDataLine object which represents an input data line from which audio data can be captured, using the method getLineInfo(DataLine.Info) of the AudioSystem class.
          Open and start the target data line to begin capturing audio data.
          Create an AudioInputStream object to read data from the target data line.
          Record the captured sound into a WAV file using the following method of the class AudioSystem:
write(AudioInputStream, AudioFileFormat.Type, File)

 

Note that this method blocks the current thread until the target data line is closed.

          Stop and close the target data line to end capturing and recording.
 This console-based program will record sound from the microphone for 60 seconds then saves the recorded sound into a file in .wav format under E:/Test/RecordAudio.wav (so make sure you created the parent directory first). You may want to save as .mp3 format, but unfortunately the Java Sound API only supports the .wav format.
You can change the record duration by modifying value of the constant RECORD_TIME at the beginning of the class.
Notice that there are two threads spawn in this program:
First thread (main thread): captures and records sound.
Second thread (the stopperthread): waits for a specified duration before closing the target data line. And because the main method is blocked by method call AudioSystem.write(), closing the target data line will continues the main method which exits the program.
Compile the program:
javac JavaSoundRecorder.java

Run it:
java JavaSoundRecorder

Output:
Start capturing...

Start recording...

Finished

And check if the file RecordAudio.wav created under E:/Test directory and play it back.
##################################################################################################################################################################################################################################################################################################################################################################
#################################################################################################################################################################################
Screenshot using Java Project
###############################
In this program we will see how we can take screenshots using a java program and save the screenshot in desired folder.
We use java.awt.Robot class to capture pixels of screen. It provides method like createScreenCapture which captures the current screen. This method returns captured image as BufferedImage object which can be saved as a file. It also uses ImageIO to save it as PNG image format. Toolkit.getDefaultToolkit().getSize() method is used to get the size of screen.
The serialVersionUID is universal version identifier for Serializable class. Thread is used so that after executing the program we can switch to the screen we want to take screenshot of. 120s is the time in seconds i.e. 2 mins.

NOTE : Please keep note of UpperCase and LowerCase in name of methods. A slight change of Case may cause errors.

How to use the program to capture Screenshot :

Write program in Notepad or any IDE.
Save it as Screenshot.java and run it on CommandPrompt.
Refer to the screenshots at end in case of any problem.
