..  Copyright (c) 2014-present PlatformIO <contact@platformio.org>
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
       http://www.apache.org/licenses/LICENSE-2.0
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

.. _board_espressif32_esp32dev:

Espressif ESP32 Dev Module
==========================

.. contents::

Hardware
--------

Platform :ref:`platform_espressif32`: Espressif Systems is a privately held fabless semiconductor company. They provide wireless communications and Wi-Fi chips which are widely used in mobile devices and the Internet of Things applications.

.. list-table::

  * - **Microcontroller**
    - ESP32
  * - **Frequency**
    - 240MHz
  * - **Flash**
    - 4MB
  * - **RAM**
    - 320KB
  * - **Vendor**
    - `Espressif <https://en.wikipedia.org/wiki/ESP32?utm_source=platformio.org&utm_medium=docs>`__


Configuration
-------------

Please use ``esp32dev`` ID for :ref:`projectconf_env_board` option in :ref:`projectconf`:

.. code-block:: ini

  [env:esp32dev]
  platform = espressif32
  board = esp32dev

You can override default Espressif ESP32 Dev Module settings per build environment using
``board_***`` option, where ``***`` is a JSON object path from
board manifest `esp32dev.json <https://github.com/platformio/platform-espressif32/blob/master/boards/esp32dev.json>`_. For example,
``board_build.mcu``, ``board_build.f_cpu``, etc.

.. code-block:: ini

  [env:esp32dev]
  platform = espressif32
  board = esp32dev

  ; change microcontroller
  board_build.mcu = esp32

  ; change MCU frequency
  board_build.f_cpu = 240000000L


Uploading
---------
Espressif ESP32 Dev Module supports the following uploading protocols:

* ``esp-prog``
* ``espota``
* ``esptool``
* ``iot-bus-jtag``
* ``jlink``
* ``minimodule``
* ``olimex-arm-usb-ocd``
* ``olimex-arm-usb-ocd-h``
* ``olimex-arm-usb-tiny-h``
* ``olimex-jtag-tiny``
* ``tumpa``

Default protocol is ``esptool``

You can change upload protocol using :ref:`projectconf_upload_protocol` option:

.. code-block:: ini

  [env:esp32dev]
  platform = espressif32
  board = esp32dev

  upload_protocol = esptool

Debugging
---------

:ref:`piodebug` - "1-click" solution for debugging with a zero configuration.

.. warning::
    You will need to install debug tool drivers depending on your system.
    Please click on compatible debug tool below for the further
    instructions and configuration information.

You can switch between debugging :ref:`debugging_tools` using
:ref:`projectconf_debug_tool` option in :ref:`projectconf`.

Espressif ESP32 Dev Module does not have on-board debug probe and **IS NOT READY** for debugging. You will need to use/buy one of external probe listed below.

.. list-table::
  :header-rows:  1

  * - Compatible Tools
    - On-board
    - Default
  * - :ref:`debugging_tool_esp-prog`
    - 
    - Yes
  * - :ref:`debugging_tool_iot-bus-jtag`
    - 
    - 
  * - :ref:`debugging_tool_jlink`
    - 
    - 
  * - :ref:`debugging_tool_minimodule`
    - 
    - 
  * - :ref:`debugging_tool_olimex-arm-usb-ocd`
    - 
    - 
  * - :ref:`debugging_tool_olimex-arm-usb-ocd-h`
    - 
    - 
  * - :ref:`debugging_tool_olimex-arm-usb-tiny-h`
    - 
    - 
  * - :ref:`debugging_tool_olimex-jtag-tiny`
    - 
    - 
  * - :ref:`debugging_tool_tumpa`
    - 
    - 

Frameworks
----------
.. list-table::
    :header-rows:  1

    * - Name
      - Description

    * - :ref:`framework_arduino`
      - Arduino Wiring-based Framework allows writing cross-platform software to control devices attached to a wide range of Arduino boards to create all kinds of creative coding, interactive objects, spaces or physical experiences

    * - :ref:`framework_espidf`
      - ESP-IDF is the official development framework for the ESP32 and ESP32-S Series SoCs.
      
      #define pintriger 14
#define pinecho 27
long duration, cm;
long distance;

#include <Arduino.h>
#include <ESP32Servo.h>
#define PIN_SERVO 13
#define PIN_SERVO 25
#define PIN_SERVO 26
#define PIN_SERVO 16
Servo myServo_1;
Servo myServo_2;
Servo myServo_3;
Servo myServo_4;

#define IN1 23
#define IN2 17

void setup () {
   
  Serial.begin (115200);
  pinMode (pintriger, OUTPUT);
  pinMode (pinecho, INPUT);
  
 pinMode(IN1, OUTPUT);
 pinMode(IN2, OUTPUT);
 
   myServo_1.attach(13);
   myServo_2.attach(25);
   myServo_3.attach(26);
   myServo_4.attach(16);
  
 myServo_1.write(90);
 myServo_2.write(90);
 myServo_3.write(90);
 myServo_4.write(90);
 }

void loop() 
{
  digitalWrite (pintriger, LOW);
  delayMicroseconds (2);
  digitalWrite (pintriger,HIGH);
  delayMicroseconds (10);
  digitalWrite (pintriger, LOW);
  duration = pulseIn(pinecho, HIGH);
  distance = (duration/2) / 29.1;
   if (distance > 20)
 {
   digitalWrite(IN1,HIGH);
   digitalWrite(IN2, LOW);
   delay(500);
   myServo_1.write (90);
   delay(500);
   myServo_3.write (180);
   delay(500);
   myServo_3.write (120);
   delay(500);
   myServo_4.write (100);
   delay(500);

 }
 else 
 {
  if (distance < 20)
   digitalWrite(IN1,LOW);
   digitalWrite(IN2, HIGH);
   delay(500);
   }          
}

  
