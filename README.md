Using Tesseract OCR in this project
Tesseract OCR (Optical Character Recognition) is used in this project to extract vehicle license plate numbers from captured images. Here’s how it fits into the system:
1. Capturing the Image
•	When motion is detected by the PIR sensor, the Raspberry Pi Camera Module captures an image of the vehicle.
2. Preprocessing the Image (Using OpenCV)
•	The captured image is processed to enhance text readability using OpenCV: 
o	Grayscale Conversion – Converts the image to grayscale for better OCR accuracy.
o	Noise Reduction – Removes unwanted background noise using filters.
o	Edge Detection – Identifies the license plate region.
o	Thresholding – Enhances contrast between text and background.
import cv2
import pytesseract

# Load the image
image = cv2.imread("car.jpg")

# Convert to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply thresholding
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Apply OCR
text = pytesseract.image_to_string(thresh, config='--psm 8')

print("Detected License Plate Number:", text)
3. Extracting the License Plate Number
•	Tesseract OCR reads the processed image and extracts the license plate number.
•	The extracted text is then compared with a database of registered vehicles.
4. Validating and Taking Action
•	If the license plate is authorized, the system logs the entry/exit.
•	If unauthorized, the system sends an SMS alert via GSM.
Tesseract ocr
Free & Open Source
Works well with OpenCV for image processing
Supports multiple languages & character sets
Runs efficiently on Raspberry Pi 5



OpenCV (Open Source Computer Vision) plays a crucial role in vehicle detection and license plate recognition in this Raspberry Pi-based Smart Parking Monitoring System. Here's how it is integrated:
1. Capturing Images When Motion is Detected
•	The PIR motion sensor triggers the Raspberry Pi to capture an image when movement is detected.
•	OpenCV is used to process the captured image.
________________________________________
2. Detecting Vehicles Using OpenCV
•	OpenCV's Haar cascades or deep learning models (YOLO, SSD, etc.) can be used to detect vehicles in an image.
•	It identifies the bounding box around a detected vehicle.
________________________________________
3. License Plate Detection & OCR using OpenCV and Tesseract
•	Once a vehicle is detected, OpenCV extracts the license plate region.
•	Tesseract OCR is used to recognize text from the plate.
________________________________________
4. Sending Alerts for Unauthorized Parking
•	If a license plate is not registered, an SMS alert is sent using the GSM module (SIM800L).
•	The system can cross-check plate numbers against a database of authorized vehicles.

Summary: How OpenCV Helps in This Project
✅ Captures images when motion is detected.
✅ Detects vehicles in real-time using OpenCV models.
✅ Extracts license plates and applies OCR for number recognition.
✅ Verifies authorization of detected vehicles.
✅ Triggers SMS alerts if unauthorized parking is detected.



Role of Raspbian OS and Python IDE in This Project
1. Raspbian OS (Now Called Raspberry Pi OS)
Why is it used?
•	Acts as the operating system for the Raspberry Pi, enabling it to run software, interact with hardware, and manage processes.
•	Provides support for GPIO pin control, allowing the RFID module, PIR sensor, GSM module, and camera to communicate efficiently.
•	Comes pre-installed with essential libraries and tools needed for hardware interfacing and image processing.
How is it used?
•	Runs background Python scripts to continuously monitor the RFID readers, motion sensors, and camera module.
•	Enables network connectivity for sending data and SMS alerts via the GSM module.
•	Stores images and logs on external USB storage or cloud-based databases.
________________________________________
2. Python IDE (Integrated Development Environment)
Why is it used?
•	Provides a user-friendly environment to write, test, and debug Python scripts used for vehicle detection, OCR processing, and SMS alerts.
•	Supports essential libraries like OpenCV, Tesseract OCR, and serial communication for hardware control.
How is it used?
•	Used to write and execute scripts that: 
o	Read RFID tag data at entry and exit points.
o	Capture images using the Raspberry Pi Camera Module when motion is detected.
o	Process images with OpenCV to detect vehicles and extract license plate numbers using Tesseract OCR.
o	Send SMS notifications via the GSM module if unauthorized parking is detected.
•	Debugging and real-time monitoring are done using the IDE to ensure the system works as expected.
