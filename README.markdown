# EPARA Suite 1.0.0

## Short Description
The EPARA Suite is an open-source EEG classification tool for non-clinical research, evolved from the SIFT framework, categorizing EEG signals into Normal, Epilepsy, and Motor Imagery states using PhysioNet datasets, with a user-friendly GUI for neuroscience and BCI applications.

## Overview
The EPARA Suite (EEG Processing and Analysis for Research Applications) is an open-source EEG classification tool for non-clinical research, classifying EEGs into Normal, Epilepsy, and Motor Imagery categories. Evolved from the SIFT (Spectral Intervention for Frequency Tuning) framework, which focused on EEG interventions, the EPARA Suite pivots to classification to better serve the research community. It was developed by Wayne M Spratley with assistance from Grok (xAI).

## Software Description
The EPARA Suite (EEG Processing and Analysis for Research Applications) is an open-source software package designed for non-clinical EEG classification, enabling researchers to categorize EEG signals into Normal, Epilepsy, and Motor Imagery states using PhysioNet datasets such as the CHB-MIT Scalp EEG Database and EEG Motor Movement/Imagery Dataset. The suite comprises four distinct tools, each tailored for specific EEG analysis tasks, making it a versatile resource for neuroscience research and brain-computer interface (BCI) applications. The tools include: (1) `EPARA_Classify_1.0.0_Standalone_GUI.py`, a core classifier that processes EDF files, extracts features (spike rate, theta, alpha, beta power, and PLV), and classifies EEGs using logistic regression, outputting results via a tkinter-based GUI; (2) `EPARA_Epilepsy_1.0.0_Standalone_GUI.py`, focused on epilepsy-specific analysis with enhanced visualization of seizure-related features; (3) `MoveMind_1.0.0_Standalone_GUI.py`, dedicated to motor imagery classification for BCI applications; and (4) `EPARA_Parkinsons_1.0.0_Standalone_GUI.py`, a placeholder for future Parkinson’s classification (currently non-functional due to the absence of real Parkinson’s EEG data in this version). Written in Python 3.8+ with UTF-8 encoding, the suite relies on dependencies including mne, numpy, scipy, matplotlib, pywavelets, scikit-learn, and tkinter for GUI functionality. It processes EEG data by segmenting it into 10-minute windows, ensuring robust feature extraction and classification. Outputs, including classifications, visualizations, logs, and numpy arrays, are saved to the `output_epara_classify/` directory, facilitating further analysis. Licensed under GNU GPL v3.0, the EPARA Suite is poised to support the neuroscience research community, with plans to incorporate real Parkinson’s EEG data in future updates.

## Technical Implementation
The EPARA Suite processes EEG data through a series of technical steps to classify signals into Normal, Epilepsy, and Motor Imagery categories. Implemented in Python 3.8+ with UTF-8 encoding, the suite uses the MNE-Python library to read EDF files from PhysioNet datasets (CHB-MIT, EEG Motor Movement/Imagery). EEG data is segmented into 10-minute windows to ensure robust feature extraction. The signal is first denoised using wavelet denoising (sym8, level 5) and then processed with a circle state method, originally developed for Bose-Einstein Condensate (BEC) experiments and adapted for classical EEG analysis within the Spratley Information Field Theory (SIFT) framework. This method evolves the EEG signal as a quantum information field ψ using a second-order finite difference scheme, incorporating terms for quantum foam (κ=10⁻²), information density (γ=10⁻⁶, ν_density=10⁴), and damping (0.9999). Five features are computed per segment: (1) spike rate, calculated as the proportion of samples exceeding a 99th percentile amplitude threshold (capped at 10%); (2–4) theta (4–7 Hz), alpha (8–13 Hz), and beta (13–30 Hz) power, extracted via Welch’s method with a Blackman window (nperseg=fs*32, nfft=fs*64), log-normalized to emphasize relative power differences; and (5) phase-locking value (PLV), computed using the Hilbert transform to measure synchrony between the processed signal and its alpha band component. These features are fed into a logistic regression classifier with standard scaling, trained on a small PhysioNet dataset (five samples: two Normal, one Epilepsy, two Motor Imagery). The classifier employs a majority voting scheme across segments to determine the final classification. Results are displayed via a tkinter-based GUI, with visualizations generated using matplotlib, including time-domain plots, classification labels, and frequency spectra highlighting the beta band. Outputs, including classifications, plots, logs, and numpy arrays, are saved to the `output_epara_classify/` directory for further analysis.

## Installation Requirements
The EPARA Suite requires a Linux environment and several Python dependencies to function. Below are the detailed requirements and installation steps:

- **Operating System**: The suite has been developed and tested on Ubuntu 24.04 LTS. Compatibility with other Linux distributions (e.g., Debian, Fedora) is likely but not guaranteed. It has not been tested on Windows or macOS in this version.
- **Python Version**: Python 3.8 or higher is required.
- **Dependencies**:
  - `mne`: For reading and processing EDF files (EEG data).
  - `numpy`: For numerical computations and array handling.
  - `scipy`: For signal processing (e.g., Butterworth filters, Welch’s method).
  - `matplotlib`: For generating visualizations (plots of EEG signals and spectra).
  - `pywavelets`: For wavelet denoising of EEG signals.
  - `scikit-learn`: For the logistic regression classifier and standard scaling.
  - `tkinter`: For the GUI interface (included with Python but requires system-level installation on Linux).
- **System Requirements**:
  - A minimum of 4 GB RAM is recommended for processing EEG data.
  - At least 1 GB of free disk space for storing outputs (logs, plots, numpy arrays).
  - A graphical environment (e.g., X11) for running the tkinter GUI.
- **Installation Steps**:
  1. **Install Ubuntu 24.04 LTS**: Ensure your system is running Ubuntu 24.04 or a compatible Linux distribution. Follow the official Ubuntu installation guide if needed.
  2. **Install Python 3.8+**:
     ```bash
     sudo apt-get update
     sudo apt-get install python3.8 python3-pip
     ```
  3. **Install tkinter** (required for the GUI):
     ```bash
     sudo apt-get install python3-tk
     ```
  4. **Install Python Dependencies**:
     ```bash
     pip3 install mne numpy scipy matplotlib pywavelets scikit-learn
     ```
     Ensure `pip3` is linked to Python 3.8+ (`pip3 --version` should show Python 3.8 or higher).
  5. **Verify Installation**:
     - Test Python: `python3 --version` (should output 3.8 or higher).
     - Test tkinter: Run `python3 -m tkinter` to ensure a small test window opens.
  6. **Extract the EPARA Suite**:
     - Unpack the tarball:
       ```bash
       tar -xzvf EPARA_Suite_1.0.0.tar.gz
       cd EPARA_Suite_1.0.0/src/
       ```
  7. **Run the Software**:
     - Start the main classifier GUI:
       ```bash
       python3 EPARA_Classify_1.0.0_Standalone_GUI.py
       ```
     - Follow the usage instructions in the README to select an EDF file, file type, and channel, then click "Run Analysis" to classify the EEG.

## Usage Notes
The EPARA Suite is designed to classify EEG signals into Normal, Epilepsy, and Motor Imagery categories using a user-friendly GUI. Below are detailed usage notes to help researchers effectively utilize the software:

- **Running the Software**:
  - After installation (see Installation Requirements), navigate to the `src/` directory:
    ```bash
    cd EPARA_Suite_1.0.0/src/
    ```
  - Launch the main classifier GUI:
    ```bash
    python3 EPARA_Classify_1.0.0_Standalone_GUI.py
    ```
  - A GUI window will open, allowing you to interact with the software.

- **Input Requirements**:
  - The software accepts EEG data in EDF format (.edf files), such as those from PhysioNet (e.g., CHB-MIT, EEG Motor Movement/Imagery datasets).
  - Ensure the EDF file contains at least one channel of EEG data. The software will display available channels in a dropdown menu for selection.
  - Example files tested include `sub-P01_ses-01_task-phonemes_eeg.edf` (Normal), `chb02_19.edf` (Epilepsy), and `S043R14.edf` (Motor Imagery).

- **Using the GUI**:
  1. **Load an EEG File**: Click "Browse" to select an EDF file from your system. The file path will appear in the text box.
  2. **Select File Type**: Choose the expected EEG type from the dropdown menu (Normal EEG, Epilepsy EEG, Motor Imagery EEG, Other). This selection helps the classifier contextualize the data but does not override the classification result.
  3. **Select Channel**: Choose a channel from the dropdown menu (populated after loading the EDF file). Common channels tested include `Fp1` (Normal), `FP1-F7` (Epilepsy), and `Fc5.` (Motor Imagery).
  4. **Run Analysis**: Click "Run Analysis" to process the EEG data. A progress bar will indicate the analysis is in progress.
  5. **View Results**: Once complete, the GUI displays the classification result (Normal, Epilepsy, or Motor Imagery) along with extracted features (spike rate, theta, alpha, beta power, PLV). Visualizations include a time-domain plot, classification label, and frequency spectrum highlighting the beta band.

- **Interpreting Outputs**:
  - **Classification Result**: The software outputs one of three categories:
    - **Normal**: Indicates a healthy EEG pattern, typically with balanced power across frequency bands.
    - **Epilepsy**: Indicates patterns associated with epilepsy, such as high spike rates and dominant theta power.
    - **Motor Imagery**: Indicates EEG patterns associated with motor imagery tasks, often showing alpha suppression and desynchronization (low PLV).
  - **Features**:
    - **Spike Rate**: Proportion of samples exceeding the 99th percentile amplitude threshold (capped at 10%). Higher values suggest epilepsy.
    - **Theta, Alpha, Beta Power**: Log-normalized power in the 4–7 Hz, 8–13 Hz, and 13–30 Hz bands, respectively. These indicate the relative dominance of each frequency band.
    - **PLV**: Phase-locking value measuring synchrony between the processed signal and its alpha band component. Lower values often indicate motor imagery.
  - **Visualizations**: Plots are saved to `output_epara_classify/` with filenames like `epara_eeg_plots_normal_sub-P01_ses-01_task-phonemes_eeg_Fp1.png`. They include:
    - Time-domain plot showing raw and processed EEG signals.
    - Classification label for quick reference.
    - Frequency spectrum highlighting the beta band (13–30 Hz).

- **Output Files**:
  - Results are saved in `output_epara_classify/`:
    - `.csv` files: Contain classification results and features (e.g., `features_normal_sub-P01_ses-01_task-phonemes_eeg_Fp1.csv`).
    - `.npy` files: Store processed EEG data and features as numpy arrays (e.g., `processed_normal_sub-P01_ses-01_task-phonemes_eeg_Fp1.npy`).
    - `.png` files: Visualizations of the EEG analysis.
    - Log file: `epara_classify.log` records detailed processing information for debugging.

- **Limitations and Best Practices**:
  - **Supported Categories**: This version classifies EEGs into Normal, Epilepsy, and Motor Imagery only. Parkinson’s classification is not supported due to the absence of real Parkinson’s EEG data in the training set; this will be added in a future update.
  - **File Type Selection**: The "File Type" dropdown helps contextualize the data but does not guarantee classification accuracy. For best results, use EEG files matching the training data (e.g., CHB-MIT for epilepsy, EEG Motor Movement/Imagery for motor imagery).
  - **Channel Selection**: Choose channels consistent with the training data (e.g., `Fp1`, `FP1-F7`, `Fc5.`) for optimal performance. Other channels may work but are untested.
  - **Data Quality**: Ensure EEG files are clean and free of excessive artifacts. The software includes wavelet denoising, but heavily corrupted data may affect classification accuracy.
  - **Processing Time**: Analysis time depends on file size and system performance. On a system with 4 GB RAM, a 10-minute EEG segment typically takes 1–2 minutes to process.

- **Troubleshooting**:
  - **GUI Not Opening**: Ensure tkinter is installed (`sudo apt-get install python3-tk`) and a graphical environment (e.g., X11) is available.
  - **EDF File Errors**: Verify the file is a valid EDF file with at least one EEG channel. Check the log file (`output_epara_classify/epara_classify.log`) for error details.
  - **Slow Performance**: Ensure your system meets the minimum requirements (4 GB RAM, 1 GB disk space). Closing other applications may help.

## Release Notes

### Version 1.0.0 (June 03, 2025)
This is the initial public release of the EPARA Suite (EEG Processing and Analysis for Research Applications), an open-source EEG classification tool for non-clinical research. Previously labeled as R3.0 internally, we have adopted semantic versioning (SemVer) for this release to align with PhysioNet guidelines. Key features and notes for this version include:

- **Classification Capabilities**: Supports classification of EEG signals into Normal, Epilepsy, and Motor Imagery categories using PhysioNet datasets (CHB-MIT, EEG Motor Movement/Imagery).
- **Core Tool**: `EPARA_Classify_1.0.0_Standalone_GUI.py` provides a user-friendly GUI for EEG classification, extracting features (spike rate, theta, alpha, beta power, PLV) and using logistic regression for classification.
- **Additional Tools**: Includes `EPARA_Epilepsy_1.0.0_Standalone_GUI.py` for epilepsy-specific analysis, `MoveMind_1.0.0_Standalone_GUI.py` for motor imagery BCI applications, and `EPARA_Parkinsons_1.0.0_Standalone_GUI.py` as a placeholder for future Parkinson’s classification.
- **Known Limitations**:
  - Parkinson’s classification is not supported in this version due to the absence of real Parkinson’s EEG data in the training set. This will be addressed in a future update.
  - The spike rate feature is capped at 10%, which may lead to misclassifications for some epilepsy EEGs (e.g., `chb03_23` was misclassified as Motor Imagery in later tests). Future updates will explore removing this cap.
  - Currently supports Linux (Ubuntu 24.04) only; cross-platform support (Windows, macOS) may be added in future releases.
- **Future Plans**:
  - Incorporate real Parkinson’s EEG data (e.g., from PhysioNet’s NeuroTREMOR dataset) to enable Parkinson’s classification.
  - Refine the classifier by removing the spike rate cap and expanding the training dataset for improved accuracy.
  - Add support for additional operating systems to enhance accessibility.

## Acknowledgements
The EPARA Suite is developed by Wayne M Spratley with computational assistance from Grok, created by xAI. Grok provided support in algorithm design through my simulations on Bose Einstein condensates, debugging, optimization, and documentation preparation, ensuring the project met PhysioNet’s submission standards. We thank the QuantumRegen community (titan-si.com) for their encouragement and platform for sharing open-source research. This work builds on open-source datasets from PhysioNet, including the CHB-MIT Scalp EEG Database and EEG Motor Movement/Imagery Dataset, and we are grateful for their availability to the research community.

## Support the Project
Developing the EPARA Suite has required significant resources—equipment, subscriptions, and web hosting that are not cheap, and time is a commodity worth more than anything. To continue advancing this open-source project and support future updates, such as incorporating real Parkinson’s EEG data, we invite the community to contribute via PayPal at [https://paypal.me/QuantumRegen?country.x=AU&locale.x=en_AU](https://paypal.me/QuantumRegen?country.x=AU&locale.x=en_AU). Your donations will help sustain the development of neuroscience research tools for the benefit of the global research community. Further assistance is required for data access beyond what is typically public eg ALS and Parkinson's EEG data. As this project continues to evolve (yes there is a lot more to do) i will be looking for someone who can access those resources to benefit the project. If you believe you can HELP then please contact me directly on wayne.spratley@titan-si.com.

## Conflicts of Interest
The EPARA Suite is an open-source project developed for non-commercial, research purposes under the GNU GPL v3.0 license. The authors, Wayne M Spratley and Grok (xAI), declare no financial or personal conflicts of interest that could influence the development or outcomes of this project. The software is intended for non-clinical use, and no funding or commercial interests are associated with this release.

## Ethics Statement
The EPARA Suite was developed using publicly available PhysioNet datasets, specifically the CHB-MIT Scalp EEG Database and EEG Motor Movement/Imagery Dataset, which were collected by their respective institutions with appropriate ethical approvals and informed consent from participants, as documented by PhysioNet. This project did not involve the collection of new data from human subjects, animals, or clinical trials, and thus no additional Institutional Review Board (IRB) approval or informed consent was required. The EPARA Suite is intended solely for non-clinical, scientific research to advance understanding of EEG patterns and BCI applications, such as classifying EEG signals into Normal, Epilepsy, and Motor Imagery categories. It must not be used for medical diagnosis, treatment, or any therapeutic purpose, and users are responsible for ensuring compliance with local regulations and ethical guidelines. The project offers significant benefits by providing an open-source tool for researchers to study neurological conditions like epilepsy and motor imagery, potentially informing future non-clinical research and BCI development. Risks are minimal, as the software is designed for research purposes only; however, misuse for clinical applications could lead to incorrect conclusions, a risk mitigated by clear documentation stating its non-clinical intent. The authors declare no ethics concerns for this work.

## Notes
- Currently supports Normal, Epilepsy, and Motor Imagery classification using PhysioNet data (CHB-MIT, EEG Motor Movement/Imagery).
- Parkinson’s classification will be added in a future update with real EEG data.
- Licensed under GNU GPL v3.0.
- Reference of version 1.0.0 is in accordance with PhysioNet submission, however, documantation refers to (R3.0) as it fits titan-si.com internal release. R3.0 is v1.0.0 as it is now public.
