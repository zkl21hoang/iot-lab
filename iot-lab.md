### 1. Instruction Power Differences

- **Attack Strategy:** Examining how power consumption in a microcontroller varies with different operations and instructions.
- **Purpose of Attack:** To capture a power trace with ChipWhisperer and identify connections between instructions and power traces.
- **Key Points to Focus On:**
  - Capturing power traces during the execution of simple instructions.
  - Comparing the power traces of different instructions.
- **Attack Approach:** 
  - Inserting code into a microcontroller and capturing the power trace during its operation.
  - Experimenting with different instructions, including empty traces, simple instructions, instruction loops, and expensive instructions.
- **Reason to be Vulnerable:** The power consumption pattern changes noticeably with different instructions, allowing for analysis and potentially identifying the instructions being executed.

### 2. Power Analysis for Password Bypass

- **Attack Strategy:** Utilizing power analysis to bypass a password.
- **Purpose of Attack:** To understand how power variations can reveal timing information and differences in code execution paths.
- **Key Points to Focus On:**
  - Capturing power traces for different password attempts.
  - Observing power trace differences when different passwords are input.
  - Identifying code paths based on the first character of the password.
  - Analyzing differences in power traces to brute-force the password.
- **Reason to be Vulnerable:** The device's power consumption varies depending on the correctness of password characters, revealing information about the correct password.

### 3. Large Hamming Weight Swings

- **Attack Strategy:** Analyzing power consumption related to data manipulation in a microcontroller.
- **Purpose of Attack:** To use power measurements for validating a device model and breaking AES using classic Differential Power Analysis (DPA).
- **Key Points to Focus On:**
  - The effect of manipulating data with high and low Hamming weights on power consumption.
  - Grouping traces based on the input data’s Hamming weight.
  - Observing, analyzing and comparing the power trace to detect data manipulation.
- **Reason to be Vulnerable:** Power consumption patterns can leak information about the data being manipulated, revealing the input values.

### 4. Recovering AES Key from a Single Bit of Data

- **Attack Strategy:** Recovering a single bit of data from the internal state of an AES implementation.
- **Purpose of Attack:** To understand device leakage and recover cryptographic information.
- **Key Points to Focus On:**
  - Creating a model of the device and feeding it observed data for each possible key value.
  - Analyzing the effect of different key guesses on the observed power traces.
  - Matching the observed data with the simulated output to find the correct key.
- **Reason to be Vulnerable:** Even a single bit of data leakage can compromise the security of the encryption, allowing key recovery.

### 5. DPA on Firmware Implementation of AES

- **Attack Strategy:** Conducting Differential Power Analysis (DPA) on AES implemented in firmware.
- **Purpose of Attack:** To distinguish traces based on the value of a bit in the SBox output, revealing the key.
- **Key Points to Focus On:**
  - Guessing a key and calculating the expected S-Box output.
  - Separating and dividing traces into groups according to specific bit values.
  - Averaging groups and calculating the Difference of Means (DoM) of them, to find the key.
- **Reason to be Vulnerable:** Variations in power consumption during the SBox operation can leak information about the key bits.

### 6. CPA on Firmware Implementation of AES

- **Attack Strategy:** Using Correlation Power Analysis (CPA) to recover the AES key from power traces.
- **Purpose of Attack:** To exploit the linear relationship between the hamming weight of the S-box output and power consumption.
- **Key Points to Focus On:**
  - Predicting the hamming weight for each output and determining correlation over traces.
  - Grouping traces based on the predicted hamming weight.
  - Using statistical methods to calculate correlation and identify the key.
- **Reason to be Vulnerable:** The hamming weight of the S-box output is linearly related to the power consumption, allowing key recovery through statistical analysis.

### 7. ChipWhisperer Analyzer CPA Attack

- **Attack Strategy:** Using ChipWhisperer's library for Correlation Power Analysis (CPA) to extract an AES key.
- **Purpose of Attack:** To demonstrate the effectiveness of CPA using correlation rather than simple analysis of differences.
- **Key Points to Focus On:**
  - Using the correlation coefficient to determine the likelihood of each key byte.
  - Analyzing the correlation coefficient for each key guess.
  - Plotting correlation over time to observe regions where S-Box lookups occur.
  - Evaluating the Partial Guessing Entropy (PGE) to determine how many traces are needed for a reliable guess.
- **Reason to be Vulnerable:** The approach successfully identifies the correct AES key with high precision using only 50 traces, showcasing the effectiveness of the CPA technique in a controlled environment.

### 8. Introduction to Clock Glitching

- **Attack Strategy:** Exploring fault injections through clock glitching to create hardware malfunctions.
- **Purpose of Attack:** To understand how inducing glitches in the clock signal can cause hardware to behave unpredictably.
- **Key Points to Focus On:**
  - Implementing clock glitches at various offsets and widths.
  - Experimenting with different combinations of glitch offsets and widths.
  - Observing the effects of these glitches on a loop counter in firmware.
  - Analyzing the outcomes to identify successful glitch parameters.
- **Reason to be Vulnerable:** Clock glitching can cause a processor to skip instructions or behave irregularly, potentially bypassing security checks or altering expected outputs.

### 9. Clock Glitching to Bypass Password

- **Attack Strategy:** Using clock glitching to bypass a password check in firmware.
- **Purpose of Attack:** To demonstrate how fault injection can be used to manipulate software execution and bypass security measures.
- **Key Points to Focus On:**
  - Implementing a glitching procedure that manipulates multiple parameters.
  - Using a multi-dimensional approach to glitching, incorporating an additional parameter (ext_offset).
  - Attempting to bypass the password check by altering the normal flow of the program, to skip critical checks.
