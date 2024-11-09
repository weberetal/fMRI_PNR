# fMRI_PNR

## General Structure

### Database Organization

The dataset is organised in a hierarchical structure that groups files by participant and type of data collected:

- **Root Folder:** `fMRI_PNR`
  - **Subfolders per Participant:** Each participant is identified by a unique `subject` ID (e.g., `s5`, `s6`).
    - **`fMRI` Folder:** Contains data on cortical activation and representation distances.
      - `distance.csv`: Representational distances in feature space for each participant.
      - `overlap.csv`: Overlap of cortical activation in voxels for each digit pair.
    - **`locognosia` Folder:** Contains touch localisation data (already published in slightly different form at: https://doi.org/10.17605/OSF.IO/QBRYZ (added here for convenience)). Only present for participants who underwent touch localization testing. Contains:
      - `absolute_error.csv`: Localization error data for each trial.
      - `misreferrals.csv`: Data on instances where a stimulus was misreferred to a different digit or the palm.

### File Contents

Each file in the dataset includes data for each participant identified by a unique `subject` ID, along with specific information relevant to each measurement type. Trials were conducted on either the left or right hand, as specified in each file where relevant. Digits are consistently coded as follows:

- **D1** = thumb  
- **D2** = index finger  
- **D3** = middle finger  
- **D4** = ring finger  
- **D5** = little finger  

**Note:** For the `fMRI` folder, all activation data is taken from the contralateral hemisphere (right hemisphere for the left hand and vice versa).

## File Descriptions

### `absolute_error.csv`

**Description:**  
This file records the absolute localisation error for each trial, quantified as the Euclidean distance (in mm) between the touch stimulus location and the participant's response. It includes localisation error data per participant and trial.

**Columns:**

| Column Name      | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `subject`        | Participant ID                                               |
| `hand`           | Hand tested (left or right)                                  |
| `trial`          | Trial number (resets for each hand)                          |
| `digit`          | Digit stimulated (D1 = thumb, D2 = index finger, etc.)       |
| `absolute_error` | Euclidean distance between the stimulus and response location (in mm) |

---

### `distances.csv`

**Description:**  
Contains data on representational distances in abstract feature space for tactile stimuli. A distance value of zero indicates indistinguishable digit representations, while one indicates total separability.

**Columns:**

| Column Name  | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `subject`    | Participant ID                                               |
| `hand`       | Hand stimulated (left or right)                              |
| `comparison` | Digits compared (D1 = thumb, D2 = index finger, etc.)        |
| `distance`   | Dissimilarity measure of functional representations between the digits |

---

### `misreferrals.csv`

**Description:**  
Records instances where a touch stimulus was misreferred to another digit or the palm. Only misreferrals are listed here, as other stimuli were correctly localised.

**Columns:**

| Column Name   | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| `subject`     | Participant ID                                               |
| `hand`        | Hand tested (left or right)                                  |
| `trial`       | Trial number (resets for each hand)                          |
| `referred_to` | Digit to which the sensation was misreferred (D1 = thumb, D2 = index finger, etc.) |

---

### `overlap.csv`

**Description:**  
Provides the voxel count for positive cortical activation at a minimal threshold (z = 2.0), showing overlap in cortical representations of specific digit pairs.

**Columns:**

| Column Name  | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `subject`    | Participant ID                                               |
| `hand`       | Hand stimulated (left or right)                              |
| `comparison` | Digits compared for overlapping activation (D1 = thumb, D2 = index finger, etc.) |
| `volume_a`   | Voxel count for the first digit                              |
| `volume_b`   | Voxel count for the second digit                             |
| `overlap`    | Voxel count for the intersection between volume_a and volume_b |

---

### `participants.csv`

**Description:**  
Demographic and group data for each participant, including injury information for those who underwent nerve repair.

**Columns:**

| Column Name         | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| `sex`               | Self-identified sex (female or male)                         |
| `handedness`        | Handedness (left or right handed) according to the Waterloo Handedness Questionnaire |
| `age_at_testing`    | Age at testing (years)                                       |
| `group`             | Participant group (patient or control)                       |
| `injured_hand`      | Hand affected by nerve repair (left, right, or none for controls) |
| `injured_nerve`     | Nerve repaired (median, ulnar, or ulnar+median; none for controls) |
| `injury_type`       | Nature of nerve transection (complete or partial; none for controls) |
| `age_at_repair`     | Age at nerve repair (years; empty for controls)              |
| `time_since_repair` | Time since repair (months; empty for controls)               |
| `locognosia`        | Indicates whether touch localization testing was conducted (if "no," data for `absolute_error.csv` and `misreferrals.csv` are absent) |
