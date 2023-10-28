# ARCHIVING
Got CRC for the regular toyota working PMV-c210 iirc. This is what you need:


    crc8 = crcmod.mkCrcFun(0x107, rev=False, initCrc=0x80, xorOut=0)
    crc_bytes = int(payload, 2).to_bytes(len(payload) // 8, byteorder='big')
    calculated_crc = crc8(crc_bytes[0:8])
    crc_bits = str(bin(calculated_crc)[2:])
   
    crc_bits= crc_bits.zfill(8)
    
    fin = "010101010011110" + differential_manchester_encode(payload + crc_bits)  + "11"

I am not putting it in, but this combined with everything in my included work shoud be enough for you to do it yourself

It appears some of these are now broken, but I don't intend on working on these anymore


# TPMS-Flipper
Generate TPMS sub files for the Flipper Zero

**Primer:**
Since approx 2009 all vehicles in the United States are required to have a method of measuring tire pressure. These sensors are called Tire Pressure Monitoring Systems (TPMS). There are two main types of TPMS, Direct and Indirect, direct sensors are mounted in the wheel and usually transmit information to the car ECU via radio frequency signals. RF TPMS transmissions are the subject of this repository. In order to prevent your vehicle's TPMS system from effecting other cars, TPMS makers rely on different encoding modulations, formats, Preambles and the TPMS sensor IDs that are set in the car's ECU.

**TPMS-Helper**
The files in this repo generate valid Flipper Zero TPMS "Low Pressure" sub files in the correct format and modulations with a user specified TPMS ID for a few TPMS types.

**Demonstration**

https://user-images.githubusercontent.com/85343771/210616359-4581ef6e-6c41-4738-b60f-186451180579.mp4

**Usage:**
You must be using Ubuntu (Debian had some weird package issues for me). Download the entire repo. Extract the TPMS folder in you home dir. Chmod +x the TPMS-helper.sh. Run it. It *should* install all needed tools and set correct permissions for Code_gen in the Resources folder. This will only happen once. Choose the TPMS type, enter the hex ID, and a Flipper sub file will be output to the Output folder. You can test it against rtl_433.

**Before the Flipper tiktokers ask, you need to generate a SPECIFIC file with the correct ID for each car/tire (you only need one tire id) or it will not work. The SUB for your car/tire will have a different ID than every other car/tire and could have a completely different encoding (very likely)**

**Credits:**

Like most projects, I built on and utilized the work of others:

- Helper Script, Schrader SMD3MA4 encoding and python modifications by Lord Daikon (me)
- Massive thanks for help wih signals analysis, python fixes, and overall wisdom from Jimilinux https://github.com/jimilinuxguy
- The excellent work of rtl_433 reversing signals was a heavily utilized resource
- PMV-107J and very useful encoding tools that are the backbone of this project from https://github.com/triq-org/tx_tools
- Citroen, and Ford from https://github.com/cdeletre/txtpms/
- subghz_ook_to_sub.py by https://github.com/evilpete/flipper_toolbox

- Also utilizes GNUradio, rtl_433, sox and python 3.10

**Contributions of protocols are welcome**

