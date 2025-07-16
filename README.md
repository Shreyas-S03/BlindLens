-----

# AI and IoT-Based Vision Assistant

This project combines AI and IoT to create a vision assistant that captures images, describes them using a large language model, and then speaks the description aloud. Additionally, it incorporates an ultrasonic sensor to detect nearby obstacles and provide alerts. This README will guide you through setting up and running both the software (AI vision assistant) and hardware (IoT sensor) components of the project.

-----

## Features

  * **Image Capture:** Utilizes your computer's webcam to capture still images.
  * **AI-Powered Image Description:** Leverages the Llava-1.5-DL AI model via Hugging Face's Gradio client to generate textual descriptions of captured images.
  * **Text-to-Speech (TTS):** Converts the image description into spoken audio using OpenAI's TTS model (specifically, the `nova` voice).
  * **Obstacle Detection (IoT):** Employs an ultrasonic sensor (HC-SR04) with an Arduino to measure distances and alert the user if an object is too close.
  * **User Interface:** A simple Kivy-based GUI allows for easy interaction to capture images and view descriptions.

-----

## Project Structure

The project consists of two main parts:

1.  **Backend Code (Python/Kivy):** Handles image capture, AI analysis, text-to-speech, and the graphical user interface.
2.  **Sensor Code (Arduino):** Manages the ultrasonic sensor for obstacle detection.

-----

## Setup and Installation

### 1\. Backend Code (Python)

To run the AI vision assistant, you'll need to set up your Python environment and install the necessary libraries.

#### Prerequisites

  * Python 3.7+
  * OpenAI API Key
  * Access to an internet connection for AI model and TTS services

#### Installation Steps

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/AI-IoT-Vision-Assistant.git
    cd AI-IoT-Vision-Assistant
    ```

    (Replace `your-username` with your actual GitHub username or the project's repository link.)

2.  **Install Python dependencies:**

    ```bash
    pip install kivy opencv-python-headless gradio_client openai pygame
    ```

      * `kivy`: For the graphical user interface.
      * `opencv-python-headless`: For webcam interaction.
      * `gradio_client`: To interact with the LLaVA model hosted on Hugging Face.
      * `openai`: For the Text-to-Speech service.
      * `pygame`: To play the generated audio.

3.  **Set up your OpenAI API Key:**
    Replace `"**"` with your actual OpenAI API key in the `backend_code.py` file:

    ```python
    OPENAI_API_KEY = "YOUR_OPENAI_API_KEY_HERE"
    ```

    **Security Note:** For production environments, it's recommended to use environment variables for sensitive API keys instead of hardcoding them directly in the script.

#### Running the Backend

To start the AI vision assistant, navigate to the project directory in your terminal and run:

```bash
python backend_code.py
```

A Kivy window will appear with a "Capture Image" button.

### 2\. Sensor Code (Arduino)

This part of the project requires an Arduino board and an HC-SR04 ultrasonic sensor.

#### Prerequisites

  * Arduino IDE
  * Arduino Board (e.g., Arduino Uno)
  * HC-SR04 Ultrasonic Sensor
  * Jumper Wires
  * Breadboard (optional but recommended)

#### Hardware Connections

Connect the HC-SR04 ultrasonic sensor to your Arduino board as follows:

  * **VCC** of HC-SR04 to **5V** on Arduino
  * **GND** of HC-SR04 to **GND** on Arduino
  * **Trig Pin** of HC-SR04 to **Digital Pin 9** on Arduino
  * **Echo Pin** of HC-SR04 to **Digital Pin 10** on Arduino
  * **LED (optional for visual alert)** to **Digital Pin 13** on Arduino (with a current-limiting resistor, typically 220 Ohm)

#### Uploading the Code

1.  Open the Arduino IDE.
2.  Copy the provided `sensor_code.ino` content into a new sketch.
3.  Select your Arduino board from **Tools \> Board**.
4.  Select the correct serial port from **Tools \> Port**.
5.  Upload the sketch to your Arduino board.

#### Serial Communication (Optional for Debugging)

The Arduino code sends '1' to the serial port if an obstacle is within the `safetyThreshold` (10 cm) and '0' otherwise. You can monitor this output using the Arduino IDE's Serial Monitor (Tools \> Serial Monitor) at a baud rate of 9600.

-----

## How to Use

### AI Vision Assistant (Python Application)

1.  Run `python backend_code.py`.
2.  Click the "Capture Image" button.
3.  The application will capture an image from your webcam, send it for analysis, and display the textual description.
4.  The description will also be spoken aloud.

### Obstacle Detection (Arduino)

1.  Once the Arduino code is uploaded, the ultrasonic sensor will continuously measure distances.
2.  If an object comes within 10 cm of the sensor, the LED connected to digital pin 13 will light up, indicating an alert.

-----

## Future Enhancements

  * **Integration of Sensor Data:** Implement communication between the Arduino (IoT) and Python (AI) components to trigger image capture or provide spoken alerts based on sensor readings. This could involve serial communication or a network protocol.
  * **Real-time Video Analysis:** Instead of single image captures, integrate a continuous video feed for real-time object detection and description.
  * **Improved UI/UX:** Enhance the Kivy interface with visual feedback for image capture, processing status, and more intuitive controls.
  * **Additional AI Models:** Explore integrating other AI models for different vision tasks (e.g., object recognition, facial recognition, sentiment analysis).
  * **Customizable Alert Thresholds:** Allow users to define the safety threshold for the ultrasonic sensor.
  * **Voice Commands:** Add functionality to trigger actions (like "capture image") using voice commands.

-----

## Contributing

Contributions are welcome\! If you have suggestions for improvements or new features, feel free to open an issue or submit a pull request.

-----

## License

This project is open-source and available under the [MIT License](https://www.google.com/search?q=LICENSE). (You might want to create a `LICENSE` file in your repository if you don't have one).

-----

## Acknowledgements

  * **Kivy:** For the cross-platform GUI framework.
  * **OpenCV:** For image and video processing capabilities.
  * **Hugging Face & Gradio:** For hosting and providing access to powerful AI models like LLaVA.
  * **OpenAI:** For their impressive Text-to-Speech API.
  * **Pygame:** For audio playback.
  * **Arduino Community:** For the accessible hardware and development environment.

-----