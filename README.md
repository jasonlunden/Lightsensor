from microbit import *
#When you import, this tells python to import a module of pre-existing 
#code from a library. It is saying you potentially want to use everything 
#from the micro bit library.
import music
#Import music module contains methods used to make and control sound.  
reading = pin1.read_analog()
#The light sensor is connected to pin 1. This code asks python to 
#define the variable (reading) and read the analogue signal from pin 1.
light = int(reading)
#The new variable (light) is defined as an integer from the (reading) 
#varible read from pin 1.
recordedLight = []   
#Creates a new list from which the readings will form and collect as 
#recordable data to be used to form the basis of the amount of light 
#recorded by the tomato plant.
for i in range(10):                 
#Adds 10 consecutive integers (light recordings) to the list.            
    recordedLight.append(light)
#This append adds each new recording to the recorded light list. 
    sleep(1000)                  
#This ensures a reading is taken each (SECOND)
print ('Light Readings:')
print (recordedLight)
#Provides a list of ten recorded light readings as per list.
#This can be used to check the function of the sensor from the back end. 
#This will not affect user interface. 
total_light = 0
#Zero is used as the start value as arrays are counted from zero and not one. 
#In order for the computer to process the equation it has to find the length 
#of the array and then add 1. Starting at zero makes this a more efficient process.
for light in recordedLight:                # For each element ...
    total_light = total_light + light      # Sums the elements in list...  
print ('Total Light Received Over 24 Hours:')
print (total_light)

recordedTemperature = []                # Creates an empty list
for i in range(10):                    # Adds 10 temperature recordings to the list
        recordedTemperature.append(temperature()) #Add new temperature value to end of list
        sleep(1000)                              #Take a temperture recording every second
print('First Temperature Reading:')
print(recordedTemperature[0])                    # Print 1st reading
print('Tenth Temperature Reading:')
print(recordedTemperature[9])                    # Print 10th reading

print("Average Temperature over 24 Hours: ")

total_Temp = 0
for temperature in recordedTemperature:                # For each element ...
        total_Temp = total_Temp + temperature                    # Sums the elements in list...

average = total_Temp / len(recordedTemperature)  # Use the len() function here to find the length of the array
print(average)                              

print ("Maximum Temperature : ")                          
print (max(recordedTemperature))                        #Printss Maximum Temperature recorded
print ("Minimum Temperature : ")
print (min(recordedTemperature))                        #Prints Minimum Temperture recorded

while True:
  if button_b.is_pressed():
    if max(recordedTemperature) > 32 or min(recordedTemperature) < 13: #if the temperture exceeded 32 degrees celsius or was under 13 degrees
      music.play(music.WAWAWAWAA)                          #play alarm
      display.show(Image.SAD)
    else:
      music.play(music.FUNK)                                                      #play song
      display.show(Image.HAPPY)
  if button_a.is_pressed():
    if total_light<300: 
      music.play(music.FUNERAL)                            #play alarm
      display.show(Image.UMBRELLA)
    else:
      music.play(music.BLUES)                                                 #play song
      display.show(Image.TARGET)    


    
