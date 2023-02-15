# PLC_Mixing_system!

Using this system as an example, let's look at programming a Siemens PLC

A schematic diagram of the 2 component mixing system is given
There are two liquid level sensors, mixer, a light signal indicating that the facility is off and two pumps, discharge valve

Open the TIA Portal and first we need to choose our PLC, so select the "1215C DC/DC/Rly" controller, this PLC is enough for our task

After your PLC is loaded, you can change settings in "General", but now we need only "**Pulse Generators(PTO/PWM) ==> StartUp**", and choose "**Warm restart - RUN**". Theat means after we turnON it will automaticly run our PLC


![1](https://user-images.githubusercontent.com/118219943/219059597-f8127726-2d9b-4caf-9bf7-943d2c58ae30.PNG)



![2](https://user-images.githubusercontent.com/118219943/219059633-939f0f0d-4736-410e-ab00-7e7c94a2d875.PNG)

Now we need the PUMP_1 and PUMP_2 pumps to turn on when the tank mix level reaches the "minimum" level, up to the L_LEVEL sensor, working until the liquid level reaches the "maximum" level of the upstream H_LEVEL sensor
MIXER mix for a short time, then the VALVE valve is opened and the mixture is drained, the level of mixture is lowered to the L_LEVEL sensor, VALVE closed and the cycle is repeated
It is important that at any time it was possible to activate an immediate stop of the equipment, in our case it would be a STOP lamp, it would light up red in case of immediate stop and all the equipment would stop working

Lets assign names, addresses and data types to our components

As Input ==> devices in this setup we will have **L_LEVEL, H_LEVEL, STOP light**
Outputs ==> **PUMP_1, PUMP_2, MIXER**

![3](https://user-images.githubusercontent.com/118219943/219059650-ed00d976-114b-4fb3-abed-53ed303fdb51.PNG)



![4](https://user-images.githubusercontent.com/118219943/219059657-c7a89ba3-b87d-4c7d-94d5-4a45fc567555.PNG)



![5](https://user-images.githubusercontent.com/118219943/219059666-eb0b6b32-5c78-43fe-b76c-581ea94ede9a.PNG)

### In Outputs we need to change adress of Outputs from %I0.0 to %Q0.0, %I0.1 to %Q0.1 and so on...
 
![6](https://user-images.githubusercontent.com/118219943/219059685-fd1d8866-4ff4-4622-87d8-8e7d6a156725.PNG)

### After our Adreese, Names, DataTypes is set now we can make some LAD codeing


![7](https://user-images.githubusercontent.com/118219943/219099424-820e3dfe-8596-4064-b67c-553c6b229528.PNG)

First we add the SR logical operator Set/Reset, here SR will perform the basic logic, namely when the "S" input receives a logical 1 on the output we get also a 1, if the "S" and "R1" inputs receive 1, then the output is 0, if it receives 0 and 1, then the output is also 0

Then let's set and normally open contacts, sign them according to the logic
When the liquid level reaches L_LEVEL the two pumps PUMP_1 and PUMP_2 will start, when the liquid level reaches H_LEVEL the pumps will stop

![8](https://user-images.githubusercontent.com/118219943/219099442-eaa98111-8c71-46d4-a06c-cf58c1ff15ba.PNG)



![9](https://user-images.githubusercontent.com/118219943/219099450-606395d6-a267-4a7c-af25-ea16460801aa.PNG)



![10](https://user-images.githubusercontent.com/118219943/219059734-5196352b-0e11-43e9-bba2-d7692e2eab8e.PNG)

Below we describe what happens after the pumps are switched off.
When the pumps are switched off, the mixing phase starts and lasts for 15 seconds in this case.
In case of an emergency stop, add a Normal open contact "STOP" between the timer and the mixer, if this is done before the timer, in case of a stop the unit will run until the end of the timer.

![11](https://user-images.githubusercontent.com/118219943/219059744-f6328058-6d6f-4791-bc5f-b4f28a5ba1c5.PNG)



![13](https://user-images.githubusercontent.com/118219943/219059747-62c32c30-ffa1-4fa9-a01a-8232c24ace36.PNG)

In the next phase we need to discharge the mixture and when the liquid level of the mixture reaches the lower sensor L_LEVEL the valve will shut off the discharge of the mixture

We also need to prescribe the logic of the "STOP" button in Network_1 and Network_3

![14](https://user-images.githubusercontent.com/118219943/219059752-7717bd86-3324-4e6a-905b-249885729522.PNG)



![15](https://user-images.githubusercontent.com/118219943/219059758-5150e74c-f28a-4fc9-8aa7-bf4e96fd4783.PNG)



![16](https://user-images.githubusercontent.com/118219943/219059773-1b07658d-ed0c-4fe8-ab79-2821e15cfaee.PNG)



![17](https://user-images.githubusercontent.com/118219943/219059780-572ecb66-61bc-48d9-87b4-6dd1dc201c18.PNG)



![18](https://user-images.githubusercontent.com/118219943/219059786-1f3f4b45-231b-4e64-b214-74d3d0d5682f.PNG)



![19](https://user-images.githubusercontent.com/118219943/219059789-db2838ce-d4d1-4510-8afc-7120d244406a.PNG)



![20](https://user-images.githubusercontent.com/118219943/219059795-051ea551-2d82-483d-ab03-cfff8c6e8b02.PNG)



![21](https://user-images.githubusercontent.com/118219943/219059797-6f56ba66-41b2-40d8-a110-d221aaa80a42.PNG)



![22](https://user-images.githubusercontent.com/118219943/219059807-96043ef6-2bf9-4eb4-9f6a-d4e854567b28.PNG)



![23](https://user-images.githubusercontent.com/118219943/219059814-e563aac2-8b28-412d-bcb1-40020170bb09.PNG)



![24](https://user-images.githubusercontent.com/118219943/219059816-c5e9b417-ebb5-428b-a2aa-e9cdb31cdaee.PNG)



