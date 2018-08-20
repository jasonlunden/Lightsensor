# When you import, this tells python to import a module of pre-existing 
# code from a library. It is saying you potentially want to use everything 
# from the micro bit library.

from microbit import *

# Import music module contains methods used to make and control sound.

import music

# The light sensor is connected to pin 1. This code asks python to 
# define the variable (reading) and read the analogue signal from pin 1.  

reading = pin1.read_analog()

# The new variable (light) is defined as an integer from the (reading) 
# varible read from pin 1.

light = int(reading)

# Creates a new list from which the readings will form and collect as 
# recordable data to be used to form the basis of the amount of light 
# recorded by the tomato plant.

recordedLight = [] 

# Adds 10 consecutive integers (light recordings) to the list. 

for i in range(10):        

# This append adds each new recording to the recorded light list.     

    recordedLight.append(light)
    
# This ensures a reading is taken each (SECOND)

    sleep(1000)                  
    
# Provides a list of ten recorded light readings as per list.
# This can be used to check the function of the sensor from the back end. 
# This will not affect user interface. 

print ('Light Readings:')
print (recordedLight)

# Zero is used as the start value as arrays are counted from zero and not one. 
# In order for the computer to process the equation it has to find the length 
# of the array and then add 1. Starting at zero makes this a more efficient process.

total_light = 0

# For each reading in the array (list) the recorded value will be added to the list 
# and total summed to create the total light variable: the total of all 10 values.
 
for light in recordedLight:               
    total_light = total_light + light      
    
# This prints the user, a sum of the ten readings taken over the twenty four hour period. 
# This way of recording and measuring light was chosen because in terms of plant growth, it is the total amount of light that a tomato 
# plant receives over a 24hour period that has the most impact on photosynthesis. 

print ('Total Light Received Over 24 Hours:')
print (total_light)

# Creates a new list from which the readings will form and collect as recordable 
# data to be used to form the basis of the temperature experienced by the tomato plant.

recordedTemperature = []                

# Adds 10 consecutive integers (temperatures) to the list. 
for i in range(10):   

# This append adds each new recording to the recorded temperature list. 
# Unlike the light sensor, the temperature function is an inbuilt capability of the micro bit. 

        recordedTemperature.append(temperature()) 
        
# Takes a temperature recording every second.       

        sleep(1000)   
        
# The first line provides a heading for the user to understand the context of the data displayed. 
# The second print ensures the device is collecting correct data and then prints 1st reading.
# The print tenth reading also acts as a heading for the tenth (final) reading for the period chosen by the user.  
# This ensures the device has collected ten correct readings and the temperature function on micro bit is operating 
# as programmed. It will then print 10th reading
        
print('First Temperature Reading:')
print(recordedTemperature[0])                    
print('Tenth Temperature Reading:')
print(recordedTemperature[9])                    

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


    
