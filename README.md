# Segmentation_and_Process_Assignment_of_Semi-StructuredEvent_Logs

Below is a short guide on how to set up the environment and run the script based on the given instructions.

## Prerequisites

- A system with the `python3.12-venv` package installed (Python 3.12)
- Permissions to install system packages (e.g., via `sudo apt install`)
- Internet access (required to download dependencies via `pip`)

## Environment Setup

1. **Install the `python3.12-venv` package:**

   ```bash
   sudo apt install python3.12-venv
   ```

2. **Create the `MGA` directory and move your data (e.g., `LogsPLG2/*.xes`) into it:**

   ```bash
   mkdir MGA
   mv LogsPLG2/ MGA/
   cd MGA/
   ```

3. **Create and activate a Python virtual environment:**

   ```bash
   python3 -m venv .
   source bin/activate
   ```

   > After running `source bin/activate`, you should see the `(MGA)` prefix in your terminal, indicating that the virtual environment is active.

## Installing Dependencies

Within the virtual environment, install the following packages (recommended to place them in a `requirements.txt`, but here they are listed as individual `pip` commands):

```bash
python3 -m pip install --upgrade pip
python3 -m pip install numpy
python3 -m pip install pandas
python3 -m pip install pm4py
python3 -m pip install Levenshtein
python3 -m pip install distance
python3 -m pip install editdistance
python3 -m pip install requests
python3 -m pip install pm4py   # (repeat if necessary)
```

> **Note:** Some packages (e.g., `pm4py`) may require additional system libraries. If errors occur, please install the missing dependencies as indicated by the error messages.

## Installing `regex-learner` (IBM)

1. **Clone the repository:**

   ```bash
   git clone https://github.com/IBM/regex-learner.git
   cd regex-learner
   ```

2. **Install the `regex-learner` tool:**

   ```bash
   python3 -m pip install .
   ```

   This package enables `xsystem`, and `XTructure`, in particular.

## Running Your Script

If your main script (e.g., `main.py`) is inside the `MGA` directory, you can run it from within this virtual environment:

```bash
cd ../MGA
python3 main.py
```


## Additional Notes

- **Deactivating the virtual environment**: After you finish working, you can exit the virtual environment by running:
  ```bash
  deactivate
  ```



# Generating Synthetic Data (Process Traces) with PLG2

This guide explains how to use PLG2 to generate synthetic process traces (logs) both with and without noise.

## 1. Installation and Setup

1. **Download PLG2**  
   - Go to the [PLG2 homepage](https://plg.processmining.it/)  
   - Click **Download** and then **Download latest version** (e.g., from [this GitHub release page](https://github.com/delas/plg/releases/tag/2.1.1))  
   - Download the file `plg-2.1.1.jar`  

2. **Move the JAR file**  
   - Place `plg-2.1.1.jar` in a convenient location (e.g., `~/Downloads/`).

3. **Run PLG2**  
   ```bash
   cd ~/Downloads/
   java -jar plg-2.1.1.jar
   ```
   PLG2 should start, displaying a GUI interface.

## 2. Creating a New Process

Before starting, create a directory called (e.g. `LogsPLG2/`) to store your logs.

1. In the PLG2 application, click **New Process**.
2. For the new process settings, configure:
   - **Maximum depth**: `8`
   - **Max AND branches**: `3`
   - **Max XOR branches**: `3`
   - Keep the other options at their default values.
3. Click **Ok**.
4. PLG2 will generate a new process model. (Sometimes the process generation might fail – if it does, an error message will appear in the terminal. Just try again.)

> **Tip**: You can repeat this step multiple times to generate multiple process models.

## 3. Generating Logs Without Noise

1. Select one of the generated processes in PLG2.
2. Click **Generate Log**.
3. In the **Log Generation** settings:
   - **Configuration presets**: Select **No noise**.
   - **Number of traces**: `50` (or your desired number of traces).
4. Generate the log file.
5. Save the resulting `.xes` file. For example, name it `LogsPLG2/log_wnoise_<processName>.xes` (or any naming convention you prefer).

> **Repeat these steps** for each process you want to generate a noise-free log from.

## 4. Generating Logs With Noise

1. Select the same (or different) process in PLG2.
2. Click **Generate Log** again.
3. In the **Log Generation** settings:
   - **Configuration presets**: Select **Noise only on the control-flow**.
   - **Number of traces**: `1000` (or your desired number of traces).
4. Generate the log file.
5. Save the resulting `.xes` file, for example as `LogsPLG2/log_noised_<processName>.xes`.

> **Repeat these steps** for each process for which you want a noisy log.

## 5. Notes

- You can generate multiple logs by creating or re-generating processes.  
- Adjust the number of traces as needed for your experiments.  
- If PLG2 fails during process generation, simply retry until a valid process is generated.  

By following these steps, you will have a set of `.xes` files representing synthetic processes (both noise-free and noisy), which can then be used in further analysis, process mining experiments, or 
testing of process discovery methods.

