# fMRI_PNR

## General Structure

### Database Organization

The dataset is organised in a hierarchical structure that groups files by participant and type of data collected:

- **Root Folder:** `fMRI_PNR`
  - **Subfolders per Participant:** Each participant is identified by a unique `subject` ID (e.g., `s5`, `s6`).
    - **`clinical` Folder:** Contains data from standardised clinical tests and questionnaires (only present for patients). Contains:
      - `dash.csv`: Disabilities of the Arm, Shoulder and Hand questionnaire.
      - `rosen_questions.csv`: Pain / discomfort domain of the Rosen score.
      - `rosen_sensory.csv`: Sensory domain of the Rosen score.
      - `sf-mpq.csv`: Short-form McGill Pain Questionnaires.
    - **`fMRI` Folder:** Contains processed fMRI data (originally we used a manually defined ROI and switched to an ROI defined by the probabilistic O'Neil surface maps during the review process). Contains:
      - `bsc_oneil.csv`: Contrasts of parameter estimate (COPE) for each digit > rest.
      - `displacement.csv`: Mean head displacement in mm for each volume of each run.
      - `distance[_oneil].csv`: Representational distances in feature space for each participant (values obtained using manual ROI are designated simply `distance.csv`).
      - `handmask-volume_oneil.csv`: Voxel count of the hand mask for each hemisphere.
      - `overlap[_oneil].csv`: Overlap of cortical activation in voxels for each digit pair (values obtained using manual ROI are designated simply `overlap.csv`).
      - `reliability-fold_oneil.csv`: Individual correlation of each runs data vs the mean of all others.
    - **`locognosia` Folder:** Contains touch localisation data (already published in a slightly different form at: https://doi.org/10.17605/OSF.IO/QBRYZ (added here for convenience)). Only present for participants who underwent touch localization testing. Contains:
      - `absolute_error.csv`: Localization error data for each trial.
      - `misreferrals.csv`: Data on instances where a stimulus was misreferred to a different digit or the palm.
    - **`vibrotactile` Folder:** Contains vibrotactile bahviour data collected outside the scanner. Contains:
      - `threshold.csv`: Median vibrotactile threshold for each digit.

### File Contents

Each file in the dataset includes data for each participant identified by a unique `subject` ID and specific information relevant to each measurement type. Trials were conducted on either the left or right hand, as specified in each file where relevant. Digits are consistently coded as follows:

- **D1** = thumb  
- **D2** = index finger  
- **D3** = middle finger  
- **D4** = ring finger  
- **D5** = little finger  

**Note:** Most activation data is taken from the contralateral hemisphere (right hemisphere for the left hand and vice versa) for the fMRI folder (except for `bsc_oneil.csv`).

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

### `bsc_oneil.csv`

**Description:** 

Contains data of the %BOLD signal change (BSC) in form of the contrast of parameter estimate (COPE) obtained using FSL FEATQUERY.

**Columns:**

| Column Name         | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| `subject`           | Participant ID                                               |
| `hand`              | Hand stimulated (left or right)                              |
| `digit`             | Digits compared (D1 = thumb, D2 = index finger, etc.)        |
| `voxel_count`       | Dissimilarity measure of functional representations between the digits |
| `min`               | Minimum COPE value                                           |
| `ten_percentile`    | 10th percentile of the COPE value                            |
| `mean`              | Mean of the COPE value                                       |
| `median`            | Median of the COPE value                                     |
| `ninety_percentile` | 90th percentile of the COPE value                            |
| `max`               | Maximum of the COPE value                                    |
| `stddev`            | Standard deviation of the COPE value                         |
| `vox_x`             | x-coordinate of peak voxel in voxel coordinates              |
| `vox_y`             | y-coordinate of peak voxel in voxel coordinates              |
| `vox_z`             | z-coordinate of peak voxel in voxel coordinates              |
| `mm_x`              | x-coordinate of peak voxel in mm coordinates                 |
| `mm_y`              | y-coordinate of peak voxel in mm coordinates                 |
| `mm_z`              | z-coordinate of peak voxel in mm coordinates                 |

---

### `dash.csv`

**Description:**  
Contains the scores for each DASH question.

**Columns:**

| Column Name | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| `subject`   | Participant ID                                               |
| `question`  | Question number according to the DASH manual                 |
| `score`     | Raw score according to the answer of the participants (blank indicates that the question was not answered) |

---

### `displacement.csv`

**Description:**  
Contains the mean relative displacement per volume per run in mm. Note that one volume around volume no. 60 is taken as reference volume by FSL).

**Columns:**

| Column Name    | Description                     |
| -------------- | ------------------------------- |
| `subject`      | Participant ID                  |
| `hand`         | Hand stimulated (left or right) |
| `run`          | Run number                      |
| `volume`       | Volume number (of run)          |
| `displacement` | Relative displacement in mm     |

---

### `distance[_oneil].csv`

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

### `handmask-volume_oneil.csv`

**Description:**

Contains the size of the probababilistic O'Neil hand mask in voxels for the left and right hemispheres.

**Columns:**

| Column Name  | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `subject`    | Participant ID                                               |
| `hand`       | Hand contralateral to hand mask (left or right)              |
| `hemisphere` | Hemisphere of the hand mask (left or right - always opposite of hand) |
| `volume`     | Volume of the hand mask in voxels                            |

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

### `overlap[_oneil].csv`

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
| `handedness`        | Handedness (left- or right-handed) according to the Waterloo Handedness Questionnaire |
| `age_at_testing`    | Age at testing (years)                                       |
| `group`             | Participant group (patient or control)                       |
| `injured_hand`      | Hand affected by nerve repair (left, right, or none for controls) |
| `injured_nerve`     | Nerve repaired (median, ulnar, or ulnar+median; none for controls) |
| `injury_type`       | Nature of nerve transection (complete or partial; none for controls) |
| `age_at_repair`     | Age at nerve repair (years; empty for controls)              |
| `time_since_repair` | Time since repair (months; empty for controls)               |
| `locognosia`        | Indicates whether touch localization testing was conducted (if "no," data for `absolute_error.csv` and `misreferrals.csv` are absent) |

---

### `reliability-folds_oneil.csv`

**Description:**

Contains the correlation values of each RSA fold for both hemispheres. Larger values means less variations between folds.

**Columns:**

| Column Name  | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `subject`    | Participant ID                                               |
| `hand`       | Hand stimulated (left or right)                              |
| `hemisphere` | Hemisphere of the hand mask (left or right - always opposite of hand) |
| `fold`       | Run under consideration                                      |
| `volume`     | Volume of the hand mask in voxels                            |

---

### `rosen_questions.csv`

**Description:**  
Contains the normalised score of the Rosen pain/discomfort domain. Higher values mean better recovery.

**Columns:**

| Column Name        | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| `subject`          | Participant ID                                               |
| `question`         | Either "hyperesthesia / alidiny" or "cold intolerance"       |
| `normalised_score` | Participant raw score divided by normative score of controls |

---

### `rosen_sensory.csv`

**Description:**  
Contains the normalised score of the Rosen sensory domain. Higher values mean better recovery.

**Columns:**

| Column Name        | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| `subject`          | Participant ID                                               |
| `subtest`          | SWM = Semmes-Weinstein monofilament, 2pd = 2-point discrimination, sti = shape-texture identification test, sollerman = reduced Sollerman hand function test |
| `normalised_score` | Participant raw score divided by normative score of controls |

---

### `sf-mpq.csv`

**Description:**  
Contains the short-form McGill pain questionnaire data. This data can be broken down into three parts: pain type (22 questions), present pain and overall pain (1 question each). Higher values mean worse pain.

**Columns:**

| Column Name | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| `subject`   | Participant ID                                               |
| `question`  | Type of pain (some are other unpleasant sensations instead), present pain level or  overall pain experience |
| `score`     | Raw score according to the answer of the participants (blank indicates that the question was not answered) |

---

### `thresholds.csv`

**Description:**

Contains the median vibrotactile thresholds in arbitrary units (0 = no vibration, 255 = maximum amplitude).

**Columns:**

| Column Name        | Description                                            |
| ------------------ | ------------------------------------------------------ |
| `subject`          | Participant ID                                         |
| `hand`             | Hand stimulated (left or right)                        |
| `digit`            | Digit stimulated (D1 = thumb, D2 = index finger, etc.) |
| `median_threshold` | Median of individual stimulation thresholds            |
