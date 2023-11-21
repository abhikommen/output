# PinMyLocations App  🗺️

Welcome to PinMyLocations (I just gave it a name 😉) - the app that simplifies location searching and pinning on Google Maps!

## Overview

PinMyLocations is a useful application designed to facilitate seamless location searching and marking on Google Maps. The app enables users to effortlessly search for locations and pin them directly onto the Google Map interface. Built with a scalable framework, it encompasses all essential use cases and implements recommended testing designs and tools for robustness and reliability.

## Built with 🛠

- **[Kotlin](https://kotlinlang.org/)** - The primary and official programming language for Android development, known for its conciseness and safety.

- **[Coroutines](https://kotlinlang.org/docs/reference/coroutines-overview.html)** - A powerful Kotlin feature for asynchronous programming, facilitating more organized and efficient code handling.

- **[Android Benchmark](https://developer.android.com/topic/performance/benchmarking/benchmarking-overview)** - A tool provided by Android for evaluating performance metrics, aiding in optimizing app speed and efficiency.

- **[Espresso](https://developer.android.com/training/testing/espresso)** - A testing framework designed for Android UI testing, providing concise and expressive syntax for writing UI tests.

- **[Dagger Hilt](https://developer.android.com/training/dependency-injection/hilt-android)** - A powerful dependency injection library by Google, seamlessly integrated with Android, simplifying DI implementation.

- **[Room](https://developer.android.com/topic/libraries/architecture/room)** - An SQLite object mapping library that provides an abstraction layer over SQLite, enabling robust database interactions.

- **[Ui Automator](https://developer.android.com/training/testing/other-components/ui-automator)** - A testing framework for Android that interacts with the device's UI components across multiple apps.

- **[Mockito](https://site.mockito.org/)** - A powerful mocking framework for Java and Kotlin that simplifies the creation of mock objects during testing.

- **[Hilt-ViewModel](https://developer.android.com/training/dependency-injection/hilt-jetpack)** - Offers dependency injection capabilities for injecting ViewModels, ensuring their smooth integration with Hilt.

- **[Leak Canary](https://square.github.io/leakcanary/)** - A memory leak detection library for Android, assisting in identifying and fixing memory leaks within the application.

## Key Features

- **Location Search:** Effortlessly search for desired locations.
- **Google Maps Integration:** Pin searched locations onto Google Maps for easy reference.
- **Scalability:** Built on a scalable framework to accommodate future enhancements.
- **Testing Designs and Tools:** Implements recommended testing designs and tools for reliability.
- **Instrumentation Testing with Espresso:** Utilizes Espresso, a powerful testing tool, for comprehensive instrumentation testing.
- **UIAutomator for Google Map Testing:** Due to Google Maps being a crucial paid service, UIAutomator is employed for thorough testing, especially for placing markers on the map.

## Instrumentation Testing : Espresso and UIAutomator

### Espresso Testing
Espresso, known for its effectiveness in instrumentation testing, serves as the primary tool for testing various aspects of the app's functionality. However, it has limitations when it comes to testing the placement of markers on Google Maps.

<p align="center">
  <img src="https://developer.android.com/static/images/training/testing/espresso.png" alt="Mockito Logo" width="200">
</p>

Espresso helps you:

- Interact with views, like clicking buttons, sliding a bar, or scrolling down a screen.
- Assert that certain views are on screen or are in a certain state (such as containing particular text, or that a checkbox is checked, etc.).

#### Turn off animations

Espresso tests run on a real device and thus are instrumentation tests by nature. One issue that arises is animations: If an animation lags and you try to test if a view is on screen, but it's still animating, Espresso can accidentally fail a test. This can make Espresso tests flaky.

For Espresso UI testing, it's best practice to turn animations off (also your test will run faster!):

1) On your testing device, go to Settings > Developer options.
2) Disable these three settings: Window animation scale, Transition animation scale, and Animator duration scale.

<p align="center">
  <img src="https://developer.android.com/static/codelabs/advanced-android-kotlin-training-testing-test-doubles/img/192483c9a6e83a0_1920.png" alt="" width="400">
</p>

### UIAutomator and Accessibility Node Info
Recognizing the importance of thoroughly testing Google Maps functionality, UIAutomator steps in. It leverages the AccessibilityService's tree of accessibility node info, which differs from Espresso's view hierarchy approach. This distinction allows UIAutomator to interact with UI elements that Espresso might not recognize, ensuring comprehensive testing of marker placements on the map.

### Why UIAutomator?
While Espresso navigates through the view hierarchy and processes all children of any ViewGroup, UIAutomator utilizes accessibility node info, which might not align one-to-one with the view hierarchy. This enables UIAutomator to identify and test views that might remain unrecognized by Espresso, especially crucial for accurate testing of Google Maps functionalities.

Our framework not only excels in UI testing with Espresso and UIAutomator but also extends its prowess to integration testing using the renowned Mockito framework.

## Integration Testing with Mockito

### What is Mockito?

Mockito is a powerful and flexible Java testing framework that simplifies the process of creating mock objects in unit tests. It plays a pivotal role in our integration testing strategy, allowing us to isolate and test components in a controlled environment.

<p align="center">
  <img src="https://raw.githubusercontent.com/mockito/mockito/main/src/javadoc/org/mockito/logo.png" alt="Mockito Logo" width="300">
</p>

Explore Mockito on [GitHub](https://github.com/mockito/mockito).

## How to Get Started

### Clone the Project

```bash
git clone https://github.com/dm-rec/Interview-Test-AndroidQA-AD-20231109.git

cd Interview-Test-AndroidQA-AD-20231109
```

### Run All Test Cases

To run all test cases seamlessly, follow these steps:

1. **Build the Project**:

    ```bash
    ./gradlew build
    
    ./gradlew clean build` - Build the entire example and execute unit and integration tests plus lint check
    
    ./gradlew installDebug` - Install the debug apk on the current connected device.
    ```

2. **Run Tests**:

    ```bash
    ./gradlew test : Local Unit Tests
    
    ./gradlew connectedAndroidTest : Instrumented Unit Tests
    ```

   These command triggers all test cases, including UI tests with Espresso and UIAutomator, as well as integration tests with Mockito.

3. **Witness the Magic**:

   Sit back and watch as our comprehensive testing suite ensures the robustness and reliability of LocationPin.


## Project Structure

<img width="560" alt="" src="https://user-images.githubusercontent.com/30040958/283680627-a1bb2f35-2d5e-4d45-8d9a-6fd4909b3704.png">

### Organized Testing
By segregating tests into specific directories (androidTest for UI-related tests and test for non-UI tests), we ensure a clear distinction between different types of testing. This organization aids in maintaining the codebase and simplifies the testing process by providing a structured environment for each type of test suite.

Absolutely! Test suites serve as a mechanism to group and run multiple tests together, allowing for efficient and comprehensive testing of different aspects of an application.

### Test Suite Overview 🧪

- **Test Suites**: A test suite is a collection of tests, either related or independent, that are executed together. It enables the seamless execution of multiple tests, facilitating efficient validation of various functionalities within an application.

#### Specific Test Suites

1. **androidTest Suite** `InstrumentationTestSuite`: To execute all instrumentation tests collectively, utilize the InstrumentationTestSuite. This suite incorporates various test cases, including scenarios where we inject our FakePlacesRepository to thoroughly validate the application's behavior even in unfavorable conditions or "unhappy paths." Running this suite ensures comprehensive coverage of instrumented tests, assessing diverse scenarios within the app's functionality.
   - <p align="center"> <img width="360" alt="" src="https://developer.android.com/static/codelabs/advanced-android-kotlin-training-testing-test-doubles/img/2ee5bcac127f3952_1920.png"></p>
   - **FakeMainActivityTest**:
      - **Purpose**: Simulates the complete **end-to-end** flow using a mocked repository.
      - **Functionality**: Doesn't make real API calls but smoothly mocks them to ensure a smooth user experience. Validates the app's behavior without interacting with actual backend services.

   - **MainActivityTest**:
      - **Objective**: Tests the complete user flow while utilizing real API endpoints and actual production-level code.
      - **Function**: Validates the application's behavior in a real-world scenario, interacting with the live backend to ensure functionality and reliability.

   - **GooglePlacesRepositoryTest**:
      - **Focus**: Core repository implementation testing.
      - **Method**: Utilizes Mockito to mock API calls and thoroughly test the repository implementation. Validates the interaction with backend services without invoking actual API endpoints.


2. **test Suite** `IntegrationTestSuite`:
   - **SearchViewModelTest**:
      - **Role**: Focuses on testing the ViewModel of the app.
      - **Importance**: Crucial in validating the ViewModel's behavior and interactions, ensuring the correct functioning of business logic and data processing within the app.

# Test Result :

This screenshot confirms successful completion of all instrumentation tests. You have the option to execute all instrumentation tests using './gradlew connectedAndroidTest' or utilize our custom test suite named 'InstrumentationTestSuite`.

<p align="center"> <img width="660" alt="" src="https://user-images.githubusercontent.com/30040958/283704927-d7b26832-1ad0-47c8-b5d9-ebc705af6fda.png"></p>

Certainly! Let's break down the functionality of each test case in the `FakeMainActivityTest` class:

### `test_CompleteUserFlow()`

**Objective:** Verify a single user flow for a search query.

**Steps:**
1. Enter a search query.
2. Initiate the search.
3. Select a search result.
4. Place a marker on the map.
5. Confirm the marker placement.

**Validation:**
- Check for the presence of the marker on the map.
- Click on the marker.

**Description:**
This test case simulates a complete user interaction flow, ensuring that the application handles user inputs correctly, performs a successful search, displays search results, allows the user to select a result, and accurately places and confirms a marker on the map.

---

### `test_CompleteUserFlow_MultipleMarkers()`

**Objective:** Test multiple search results and place multiple markers on the map.

**Steps:**
1. Run the user flow for 5 search results.
2. Place 5 markers on the map.

**Validation:**
- Verify that the number of markers matches the number of search results.

**Description:**
This test case extends the previous one by iterating through multiple search results, placing markers on the map for each result, and ensuring that the count of markers corresponds to the expected number of search results.

---

### `test_Fix_InvalidLocationSearch_SpecialCharacters()`

**Objective:** Examine behavior with an invalid search query containing special characters.

**Steps:**
1. Enter an invalid search query.
2. Initiate the search.
3. Handle UI based on API responses.

**Validation:**
- Verify UI behavior in case of invalid queries.
- Check for specific messages on the UI.

**Description:**
This test case assesses how the application handles invalid search queries, particularly those containing special characters. It ensures that the UI provides appropriate feedback and displays specific messages when necessary.


**⚠️ Observation** : During testing, a noteworthy observation was made. When a user attempted to search for an invalid string, such as ($%^&), they encountered a list dialog displaying an evidently empty result. Since there was no option for the user to select from the results, and returning to the activity from the dialog was not possible, the user found themselves in a state where they were essentially unable to proceed within the app. This situation is illustrated in the screenshot below.

<p align="center"> <img width="260" alt="" src="https://user-images.githubusercontent.com/30040958/283721079-c56b8ed4-7509-4f5f-be4d-9895f5a0352e.png"></p>

**✅ Fix** To maintain a seamless user flow and address this issue, a fix has been implemented. Now, if the Google Places API returns an empty result, the app no longer displays an empty result to the user. Instead, it presents an informative toast message, ensuring that users receive meaningful feedback and are not left stuck in an unresponsive state, as illustrated below.

<p align="center"> <img width="260" alt="" src="https://user-images.githubusercontent.com/30040958/283720803-a160b826-fa0f-4afc-8812-593590c4a7bd.png"></p>

---

### `test_FailureLocationSearch()`

**Objective:** Test behavior in case of API failures or no internet connection.

**Steps:**
1. Enter an invalid search query.
2. Initiate the search.
3. Handle UI based on API responses.

**Validation:**
- Check UI behavior in case of API failures.
- Ensure specific messages are displayed.

**Description:**
This test case evaluates the application's response to API failures or lack of internet connection. It verifies that the UI provides clear feedback to the user in such scenarios, displaying informative messages as needed.

---

These test cases collectively cover a range of scenarios, including successful user interactions, handling multiple search results, addressing issues with invalid queries, and managing failures related to the API or internet connection.

#### Scalable Framework Consideration

The introduction of the `test` directory, even with a single test (`SearchViewModelTest`), demonstrates the scalability of the testing framework. By segregating different types of tests into dedicated directories (`androidTest` and `test`), we establish a foundation for expanding and enhancing test coverage as the application evolves. This separation ensures a structured and scalable testing environment, accommodating future testing needs and maintaining the reliability of the application's codebase.

# Performance Inspection Report  🐎

## Overview:

In this performance inspection report, a thorough evaluation of the app's performance has been conducted. The assessment encompasses three distinct methodologies to comprehensively cover various aspects: passive testing, manual testing, and automated testing.

This report presents an in-depth performance analysis conducted on the Realme device (RMX3471) running Android 13. The analysis focuses on passive testing methodologies, utilizing logs and system snapshots to assess various performance metrics, including processor and RAM states.

This report provides a detailed analysis of the performance testing conducted on a Realme device (RMX3471) running Android 13.

## Device Configuration:

- **Device Model:** Realme (RMX3471)
- **Android Version:** 13

## Processor and RAM State Snapshot:

```
procs ------------memory------------ ----swap--- -----io---- ---system-- ----cpu----
 r  b    swpd    free   buff   cache    si    so    bi    bo    in    cs us sy id wa
 6  0 1602784  114136   3952 2027696    21    30    92    40     1   563 28 29 43  0
```

- **Procs:** Number of processes running
- **Memory:** Memory usage metrics (swpd, free, buff, cache)
- **Swap:** Swap space metrics (si, so)
- **IO:** Input/output metrics (bi, bo)
- **System:** System-related metrics (in, cs)
- **CPU:** CPU usage breakdown (us, sy, id, wa)

## Passive Testing:

Passive testing involves the observation of an application's performance without actively inducing specific scenarios or interactions. It relies on monitoring system logs, visual cues, or other indicators to identify potential performance issues without directly interacting with the application.

### 1) Frame Drop Analysis (Log: `package:mine tag: Choreographer`):

- **Objective:** Identify frame drops during activity loading.
- **Observations:** Multiple test runs revealed an average of approximately 45 frames skipped per test.
- **Screenshot:**

<p align="center">
<img src="https://user-images.githubusercontent.com/30040958/283680538-8f216598-ada1-4845-8381-0125e6f533d2.png" alt="" style="width: 80%;"> </p>

### 2) OpenGL Renderer Log Analysis (Log: `package:mine tag: OpenGLRenderer`):

- **Objective:** Check for logs indicating rendering issues.
- **Observations:** No logs under "OpenGLRenderer" (Davey) were observed, indicating a positive sign with no rendering issues.
- **Conclusion:** The absence of logs suggests smooth rendering without rendering errors.

<p align="center">
<img src="https://user-images.githubusercontent.com/30040958/283680572-1c5fc2f1-bb21-4472-8705-d47a521fcda1.png" alt="" style="width: 80%;"> </p>


### 3) Activity Display Time Analysis (Log: `tag: ActivityTaskManager Displayed`):

- **Objective:** Assess the time taken to initiate the displayed activity.
- **Observations:** The log indicated an initiation time of approximately 860ms, close to 1 second.
- **Conclusion:** The initialization time falls within an acceptable range, but improvements could be considered for enhanced user experience.

<p align="center">
<img src="https://user-images.githubusercontent.com/30040958/283680593-ee1dc9fc-1f2b-4690-a625-136eef72dae6.png" alt="" style="width: 80%;"> </p>


## Manual App Performance Review

In the upcoming steps, we'll delve into a manual review of the app's performance. Once the specific area of your app to scrutinize has been determined, a variety of tools can be employed to precisely identify the ongoing processes.

Given that our app involves making API calls and rendering maps on the device, a multitude of factors come into play. For manual evaluation, we'll leverage the **Android Profiler** tool integrated into Android Studio. This offer valuable insights into your app's performance, allowing you to customize the level of detail—whether exclusively focusing on your app or when dealing with devices predating Android 9.

### Memory Profiling :

For monitoring our app's memory usage, we use Memory Profiler—a component within Android Profiler. It helps identify memory leaks and churn that cause performance issues like stuttering or crashes. The tool displays real-time graphs of the app's memory use, allowing us to capture heap dumps, force garbage collections, and track memory allocations.

We've also integrated LeakCanary into our project—a tool that detects and captures memory leaks on the fly. This addition enables us to proactively manage memory-related issues within our app.

<p align="center">  
<img src="https://miro.medium.com/v2/resize:fit:1400/1*2P3cfQquB98somTdTBlaag.png" alt="" style="width: 70%;"> </p>  

The screenshot illustrates the memory footprint during a specific user flow within the app. Initially, upon app launch, the memory usage remains stable. However, when initiating a location search, there's a noticeable spike in memory usage, peaking at approximately **293MB**, followed by swift garbage collection, after which the app functions smoothly again.

You can access the memmory file **memory-20231121T031409.heapprofd** file, which can be loaded into Android Studio for analysis or visualized using **Perfetto**. This file provides detailed insights into the memory behavior during this user flow, aiding in further analysis and optimization.

<p align="center">  
<img src="https://user-images.githubusercontent.com/30040958/284396887-2b94adba-1b1a-4e5c-9b03-a602adba386d.png" alt="" style="width: 80%;"> </p>  

💁🏻 : The pink ball represents screen click or in our case map click and drag;

The figures displayed at the top of the Memory Profiler (figure 2) represent the private memory pages committed by your app according to the Android system. This count specifically excludes pages shared with the system or other applications.

<p align="center">  
<img src="https://user-images.githubusercontent.com/30040958/284396879-ab2f22b8-0d08-4fcd-8a26-caa63f00a954.png" alt="" style="width: 80%;"> </p>  


Here's a breakdown of the memory count categories:

-   **Java:** Memory attributed to objects allocated from Java or Kotlin code.
    
-   **Native:** Memory allocated from C or C++ code. Note: Even without using C++, some native memory might be visible due to the Android framework's use of native memory for handling tasks like image assets, despite the primary code being in Java or Kotlin.
    
-   **Graphics:** Memory utilized for graphics buffer queues essential for displaying pixels on the screen. This includes GL surfaces, textures, etc. Notably, this memory is shared with the CPU and isn't dedicated GPU memory.
    
-   **Stack:** Memory utilized by both native and Java stacks within your app, often correlated with the number of threads your app runs.
    
-   **Code:** Memory used for app-related code and resources, encompassing dex bytecode, optimized or compiled dex code, .so libraries, and fonts.
    
-   **Others:** Memory utilized by your app that the system cannot precisely categorize.
    
-   **Allocated:** The count of Java/Kotlin objects allocated by your app, excluding objects allocated in C or C++.

  ## Networking Profiling with App Inspector

In the context of LocationPin, where internet connectivity is essential for location search and pinning, it is crucial to assess network performance. Testing network performance helps identify potential issues such as unwanted network calls or insecure connections. Additional considerations include:

- **Unwanted Network Calls:** Ensuring that there are no unnecessary or unintended network requests being made by the application.

- **Connection Security:** Verifying the security of the network connection to safeguard sensitive information.

- **Response Time:** Evaluating the time taken for requests and responses to ensure optimal user experience.

To facilitate this comprehensive network analysis, we've employed the powerful Android Studio tool, App Inspector. This tool allows us to visualize all the network calls made by our application, providing detailed information about each call, including request details, response content, and response times.

Refer to the following image for a snapshot of how App Inspector presents a clear overview of the application's network activity, aiding in the identification and resolution of potential networking issues.

<p align="center">  
<img src="https://user-images.githubusercontent.com/30040958/284399726-20197598-30de-4efb-980f-40c481abf7f5.png" alt="" style="width: 80%;"> </p>  

## CPU Profiling for App Analysis and Battery Consumption

For a thorough examination of our app's performance, including CPU usage, battery consumption, and real-time thread activity, we've harnessed the capabilities of the CPU Profiler. This tool allows us to monitor these crucial metrics as users interact with our app.

You can delve into the specifics through various profiling methods:

- **Real-time Interaction Monitoring:** Gain insights into CPU usage, battery consumption, and thread activity as users engage with the app in real time.

- **Recorded Method Traces:** Access detailed information about method execution over time, aiding in pinpointing performance bottlenecks and optimizing code.

- **Function Traces:** Explore recorded traces that provide a granular view of function-level activity, enabling a deeper understanding of the app's behavior.

- **System Traces:** Analyze recorded system traces to comprehend the overall system-level interactions and resource utilization.

<p align="center">  
<img src="https://user-images.githubusercontent.com/30040958/284401604-34aa198a-6a8b-47d3-9a15-c3c9da4996b9.png" alt="" style="width: 80%;"> </p>  


## Automated Performance Testing
Beyond manual inspection, we've implemented automated testing procedures to gather and consolidate performance data. These automated tests offer insights into the user experience, allowing us to detect potential regressions effectively.

Our chosen tool for this purpose is the official Android BenchMark, which conducts automated tests directly on the device. It generates comprehensive reports detailing various performance metrics. By leveraging this tool, we can continuously monitor app performance, ensuring that it aligns with user expectations and swiftly identifying any regressions that may arise.

<p align="center">  
<img src="https://user-images.githubusercontent.com/30040958/284478671-17ecf93d-6a58-467b-b15d-be57ae076069.png" alt="" style="width: 80%;"> 
</p> 


  
## Recommendations and Further Analysis:  
  
1. **Frame Drop Optimization:**  
- Investigate and address factors contributing to frame drops during activity loading.  
- Consider optimizing resource-intensive tasks or rendering processes.  
  
2. **Performance Monitoring:**  
- Implement continuous monitoring of system logs to identify potential performance bottlenecks.  
- Explore additional logging tags and metrics to obtain a more comprehensive performance overview.  
  
3. **Activity Initialization Time:**  
- Evaluate opportunities to optimize the initialization time further, aiming for a seamless user experience.  
- Consider asynchronous loading or background processes to reduce perceived loading times.  
  
4. **Additional Testing Scenarios:**  
- Conduct additional testing scenarios, such as stress testing or scenarios with varying network conditions, to assess the app's robustness in different environments.  
  
5. **Regular Performance Checks:**  
- Establish a routine for regular performance checks to ensure ongoing optimization efforts and a consistently high-quality user experience.  
  
This detailed performance analysis, incorporating the definition and results of passive testing, serves as a valuable resource for identifying areas of improvement and guiding future optimization efforts.  
  
# Understanding Performance in Production  
  
### Android Vitals  
  
Android vitals is a tool designed to enhance your app's performance by providing alerts when specific performance metrics surpass predefined thresholds. This feature serves as a valuable resource in optimizing your application's responsiveness and overall user experience.  
  
### Firebase Performance SDK  
  
The Firebase Performance SDK plays a crucial role in gathering diverse metrics related to your app's performance. Utilizing this SDK, you can measure various aspects, such as the time it takes for the app to transition from being opened to becoming responsive. This capability aids in the identification of potential startup bottlenecks, allowing for targeted improvements in your app's performance.  
  
### Getting Started  
  
To integrate Android vitals and the Firebase Performance SDK into your project, refer to the relevant documentation provided by Google.  
  
- [Android Vitals Documentation](https://developer.android.com/topic/performance/vitals)  
- [Firebase Performance SDK Documentation](https://firebase.google.com/docs/perf-mon/get-started-android)  
  
Feel free to explore these resources to unlock the full potential of performance optimization for your Android application.  
  
  
## Contribute and Improve  
  
We welcome contributions and feedback from the community! Whether it's bug reports, feature requests, or direct contributions, your input is valuable in enhancing LocationPin.  
  
## License

    Copyright 2022 DriveMode.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
  
---  
  
Elevate your testing game with LocationPin. Join us in creating a reliable and efficient location mapping experience! 🚀🌍  
  
Thanks for reading, Abhi ^_^
