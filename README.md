# BulkAutoregulation

This repository contains the code associated with the paper:

**Intraoperative utilization of high-resolution data for cerebral autoregulation: a feasibility study**

Ryan L. Melvin, Jayvee R. Abella, Raajen Patel, Joshua M. Hagood, Dan E. Berkowitz, and Domagoj Mladinov

[Published in *British Journal of Anaesthesia*, Volume 128, Issue 3, March 2022, Pages e217–e219.](https://doi.org/10.1016/j.bja.2021.10.035)

---

## Overview

This project demonstrates the feasibility of automated intraoperative monitoring and analysis of cerebral autoregulation using high-resolution data collected during cardiac surgery. The code processes arterial blood pressure (ABP) and near-infrared spectroscopy (NIRS) signals to compute cerebral autoregulation indices (COx and HVx), fit autoregulation curves, and calculate the lower and upper limits of autoregulation and optimal arterial blood pressure (ABP) for patients.

---

## Features

- **Batch Processing**: Automates the processing of multiple patient data sets.
- **Autoregulation Indices Calculation**: Computes COx and HVx indices using high-resolution intraoperative data.
- **Curve Fitting with Quality Checks**: Fits autoregulation curves with built-in quality checks as per established protocols (Aries et al., 2012).
- **Report Generation**: Generates LaTeX reports with figures and tables summarizing the results for each patient.
- **Performance Metrics**: Calculates and reports time outside autoregulation limits and area under the curve metrics.

---

## Requirements

- **Python**: 3.8.5 or higher
- **Python Packages**:
  - pandas
  - numpy
  - scipy
  - matplotlib
  - jupyter
  - IPython
  - ipywidgets
  - streamz
  - holoviews
  - sqlalchemy
  - pyodbc
  - datetime
  - Pillow (PIL)
  - shutil
  - re
  - sys

- **Sickbay™ Package**: Provided by Medical Informatics Corp. (MIC). Contact [jayvee.abella@michealthcare.com](mailto:jayvee.abella@michealthcare.com) to obtain access.

---

## Installation

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/UABPeriopAI/BulkAutoregulation.git
   cd BulkAutoregulation
   ```

2. **Install Python Dependencies**:

   Ensure you have [pip](https://pip.pypa.io/en/stable/installing/) installed, then run:

   ```bash
   pip install -r requirements.txt
   ```

3. **Obtain Sickbay™ Package**:

   The `sickbay` Python package is proprietary and available upon request from MIC.

   - Contact [jayvee.abella@michealthcare.com](mailto:jayvee.abella@michealthcare.com) to request access.
   - Follow the instructions provided to install the `sickbay` package.

---

## Usage

1. **Prepare Input Data**:

   - Create a CSV file named `patient_list.csv` with the following columns:
     - `MRN`: Medical Record Number
     - `AnesthesiaStart`: Start time of anesthesia (format: `YYYY-MM-DD HH:MM:SS`)
     - `AnesthesiaEnd`: End time of anesthesia (format: `YYYY-MM-DD HH:MM:SS`)
     - `Patients Name`: (Optional)
     - `Procedure`: (Optional)

2. **Configure User Inputs**:

   In the script or notebook, adjust the following variables as needed:

   ```python
   outdir = '/output/'  # Output directory
   patient_list_file = 'patient_list.csv'  # Input patient list file
   algos_to_try = ['HVx', 'COx']  # Autoregulation indices to calculate
   algo_cbf_lims = [(0,100), (-9,11)]  # Limits for cerebral blood flow signals
   abp_limits = (0,250)  # Limits for arterial blood pressure signals
   ca_threshold = 0.3  # Threshold for determining limits of autoregulation
   ```

3. **Sign In to Sickbay™ Server**:

   Replace `'sickbay_url_as_string'` with your actual Sickbay™ server URL:

   ```python
   sickbay.sign_in('sickbay_url_as_string')
   ```

   Authentication may be required as per MIC's instructions.

4. **Run the Script or Notebook**:

   - Execute the script or run all cells in the Jupyter notebook.
   - The code will process data for each patient listed in `patient_list.csv`.

5. **View Outputs**:

   - Generated LaTeX reports and figures will be saved in the specified `outdir`.
   - A CSV file `GoodCurveData.csv` containing calculated values for each patient will be created.
   - The average runtime per patient will be displayed.

---

## Understanding the Code

- **Import Required Packages**: Imports all necessary Python packages, including `sickbay`.
- **Utility Functions**:
  - `Capturing`: Captures standard output for logging.
  - `prepare_figure_lines`: Prepares LaTeX code for including figures in reports.
  - `report_patient_curves`: Wrapper function to process patient data, compute indices, generate curves, perform quality checks, and output results.
- **Data Processing Steps**:
  1. Retrieve and preprocess ABP and CBF data using `sickbay`.
  2. Compute cerebral autoregulation indices (COx and HVx).
  3. Bin pressure values and exclude bins based on data percentage.
  4. Fit a second-order polynomial to mean CA index values.
  5. Apply quality checks as per Aries et al. (2012).
  6. Determine lower and upper limits of autoregulation using the specified threshold.
- **Report Generation**:
  - LaTeX reports are created with figures of the autoregulation curves and tables summarizing key metrics.
  - Warnings and failed quality checks are noted in the reports.

---

## Notes

- **Sickbay™ Integration**: Direct access to patient data via Sickbay™ is required. Ensure compliance with all relevant data protection and privacy regulations.
- **Quality Assurance**: The code includes quality checks to ensure the validity of the autoregulation curves and indices.
- **Customization**: Parameters such as signal limits and thresholds can be adjusted to suit different data sets or research needs.

---

## References

- **Aries et al., 2012**: Continuous determination of optimal cerebral perfusion pressure in traumatic brain injury. *Critical Care Medicine.*, 40(8), 2456-2463.
- **Brady et al., 2010**: Monitoring cerebral blood flow pressure autoregulation in pediatric patients during cardiac surgery. *Stroke*, 41(9), 1957-1962.
- **Lee et al., 2009**: Cerebrovascular reactivity measured by near-infrared spectroscopy. *Stroke*, 40(5), 1820-1826.
- **Lee et al., 2013**: Cerebrovascular autoregulation in pediatric moyamoya disease. *Pediatric Anesthesia*, 23(5), 547-556.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Contact Information

For questions or comments, please contact:

- **Ryan L. Melvin** - [rlmelvin@uab.edu](mailto:rlmelvin@uab.edu)
- **Domagoj Mladinov** - [dmladinov@uabmc.edu](mailto:dmladinov@uabmc.edu)

---

## Acknowledgments

- Thanks to the IT group in the Department of Anesthesiology and Perioperative Medicine and the Health Services Information Systems team at the University of Alabama at Birmingham (UAB) for integrating Sickbay™ into the cardiovascular operating rooms.
- Collaborators at Medical Informatics Corp. (MIC) for providing support with the Sickbay™ platform.

---

## Citation

If you use this code or find it helpful in your research, please cite:

> Melvin RL, Abella JR, Patel R, Hagood JM, Berkowitz DE, Mladinov D. Intraoperative utilization of high-resolution data for cerebral autoregulation: a feasibility study. *British Journal of Anaesthesia*, Volume 128, Issue 3, March 2022, Pages e217–e219.

---

## Troubleshooting and Support

- **Common Issues**:
  - **Access Denied**: Ensure you have proper credentials and permissions to access the Sickbay™ server and data.
  - **Missing Packages**: Check that all required Python packages are installed and up to date.
  - **Data Format Errors**: Verify that the input CSV file is correctly formatted.

- **Support**:
  - For issues related to the Sickbay™ platform or package, contact MIC support or [jayvee.abella@michealthcare.com](mailto:jayvee.abella@michealthcare.com).
  - For code-related questions, open an issue in this repository or contact the authors directly.

---

## Future Work

- **Real-Time Implementation**: Plans to implement real-time autoregulation calculations using streaming data from the Sickbay™ platform.
- **Optimizations**: Improving curve generation success rates through enhanced filtering and data processing techniques.
- **Expanded Studies**: Utilizing this code for larger-scale studies to validate findings and inform clinical practices.

