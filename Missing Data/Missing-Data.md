---
title: "Missing Data"
author: "Syed Jafar Raza Rizvi <br> NSID: cfr954 <br> Student ID: 11344782"
output:
  html_document:
    keep_md: true
date: "2025-02-11"
zotero: true
bibliography: scholar.bib
---


# 1. **Dataset Exploration**  
   - Load the provided health administrative dataset.  
   - Explore the dataset to identify the extent, patterns, and potential reasons for missing data.  
   - Summarize findings using tables, charts, or heatmaps to visualize missingness.  
   
## - Load the provided health administrative dataset.

``` r
data<-read.csv("can_path_data.csv")
# data <- data %>% select(ID:HS_GEN_HEALTH, PA_TOTAL_SHORT, PM_BMI_SR, contains("_EVER"), contains("WRK_"))
```

## - Explore the dataset to identify the extent, patterns, and potential reasons for missing data.

### Explore Dataset 

**Check the structure of the dataset**


``` r
dim(data)
```

```
## [1] 41187   440
```

``` r
df_info <- data.frame(
  Variable = names(data), 
  Type = sapply(data, class)  # Gets the data type of each variable
)
print(df_info, row.names = FALSE)  # Print full output
```

```
##                             Variable      Type
##                                   ID character
##                         ADM_STUDY_ID   integer
##                           SDC_GENDER   integer
##                         SDC_AGE_CALC   integer
##                   SDC_MARITAL_STATUS   integer
##                        SDC_EDU_LEVEL   integer
##                    SDC_EDU_LEVEL_AGE   integer
##                           SDC_INCOME   integer
##                    SDC_INCOME_IND_NB   integer
##              SDC_HOUSEHOLD_ADULTS_NB   integer
##            SDC_HOUSEHOLD_CHILDREN_NB   integer
##                        HS_GEN_HEALTH   integer
##                HS_ROUTINE_VISIT_EVER   integer
##                HS_ROUTINE_VISIT_LAST   integer
##                 HS_DENTAL_VISIT_EVER   integer
##                 HS_DENTAL_VISIT_LAST   integer
##                         HS_FOBT_EVER   integer
##                         HS_FOBT_LAST   integer
##                          HS_COL_EVER   integer
##                          HS_COL_LAST   integer
##                          HS_SIG_EVER   integer
##                          HS_SIG_LAST   integer
##                      HS_SIG_COL_EVER   integer
##                      HS_SIG_COL_LAST   integer
##                        HS_POLYP_EVER   integer
##                          HS_PSA_EVER   integer
##                          HS_PSA_LAST   integer
##                 MH_CHILDREN_FATHERED   integer
##                  WH_MENSTRUATION_AGE   integer
##               WH_CONTRACEPTIVES_EVER   integer
##                WH_CONTRACEPTIVES_AGE   integer
##           WH_CONTRACEPTIVES_DURATION   integer
##                         WH_GRAVIDITY   integer
##                    WH_PREG_FIRST_AGE   integer
##                          WH_PREG_CUR   integer
##                       WH_PREG_CUR_WK   integer
##                     WH_PREG_LAST_AGE   integer
##            WH_BREASTFEEDING_DURATION   integer
##                          WH_HFT_EVER   integer
##                    WH_MENOPAUSE_EVER   integer
##                  WH_MENOPAUSE_REASON   integer
##                     WH_MENOPAUSE_AGE   integer
##                          WH_HRT_EVER   integer
##                           WH_HRT_AGE   integer
##                      WH_HRT_DURATION   integer
##                 WH_HYSTERECTOMY_EVER   integer
##                  WH_HYSTERECTOMY_AGE   integer
##                 WH_OOPHORECTOMY_EVER   integer
##                WH_OVARIES_REMOVED_NB   integer
##                   WH_BI_OOPHORECTOMY   integer
##                  WH_OVARIES_LAST_AGE   integer
##                          HS_MMG_EVER   integer
##                          HS_MMG_LAST   integer
##                          HS_PAP_EVER   integer
##                          HS_PAP_LAST   integer
##                         DIS_HBP_EVER   integer
##                          DIS_HBP_AGE   integer
##                           DIS_HBP_TX   integer
##                          DIS_MI_EVER   integer
##                           DIS_MI_AGE   integer
##                            DIS_MI_TX   integer
##                      DIS_STROKE_EVER   integer
##                       DIS_STROKE_AGE   integer
##                        DIS_STROKE_TX   integer
##                      DIS_ASTHMA_EVER   integer
##                       DIS_ASTHMA_AGE   integer
##                        DIS_ASTHMA_TX   integer
##                   DIS_EMPHYSEMA_EVER   integer
##                    DIS_EMPHYSEMA_AGE   integer
##                     DIS_EMPHYSEMA_TX   integer
##                          DIS_CB_EVER   integer
##                           DIS_CB_AGE   integer
##                            DIS_CB_TX   integer
##                        DIS_COPD_EVER   integer
##                         DIS_COPD_AGE   integer
##                          DIS_COPD_TX   integer
##                         DIS_DEP_EVER   integer
##                          DIS_DEP_AGE   integer
##                        DIS_DIAB_EVER   integer
##                        DIS_DIAB_TYPE   integer
##                         DIS_DIAB_AGE   integer
##                          DIS_DIAB_TX   integer
##                          DIS_LC_EVER   integer
##                           DIS_LC_AGE   integer
##                          DIS_CH_EVER   integer
##                           DIS_CH_AGE   integer
##                       DIS_CROHN_EVER   integer
##                        DIS_CROHN_AGE   integer
##                          DIS_UC_EVER   integer
##                           DIS_UC_AGE   integer
##                         DIS_IBS_EVER   integer
##                          DIS_IBS_AGE   integer
##                      DIS_ECZEMA_EVER   integer
##                       DIS_ECZEMA_AGE   integer
##                         DIS_SLE_EVER   integer
##                          DIS_SLE_AGE   integer
##                          DIS_PS_EVER   integer
##                           DIS_PS_AGE   integer
##                          DIS_MS_EVER   integer
##                           DIS_MS_AGE   integer
##                          DIS_OP_EVER   integer
##                           DIS_OP_AGE   integer
##                   DIS_ARTHRITIS_EVER   integer
##                    DIS_ARTHRITIS_AGE   integer
##                  DIS_ARTHRITIS_TYPE1   integer
##                  DIS_ARTHRITIS_TYPE2   integer
##                  DIS_ARTHRITIS_TYPE3   integer
##                      DIS_CANCER_EVER   integer
##                          DIS_CANCER1   integer
##                      DIS_CANCER1_AGE   integer
##                       DIS_CANCER1_TX   integer
##                 DIS_CANCER1_TX_CHEMO   integer
##                   DIS_CANCER1_TX_RAD   integer
##                  DIS_CANCER1_TX_SURG   integer
##                 DIS_CANCER1_TX_OTHER   integer
##                     DIS_HBP_FAM_EVER   integer
##                      DIS_MI_FAM_EVER   integer
##                  DIS_STROKE_FAM_EVER   integer
##                  DIS_ASTHMA_FAM_EVER   integer
##               DIS_EMPHYSEMA_FAM_EVER   integer
##                      DIS_CB_FAM_EVER   integer
##                    DIS_COPD_FAM_EVER   integer
##                     DIS_DEP_FAM_EVER   integer
##                    DIS_DIAB_FAM_EVER   integer
##                      DIS_LC_FAM_EVER   integer
##                      DIS_CH_FAM_EVER   integer
##                   DIS_CROHN_FAM_EVER   integer
##                      DIS_UC_FAM_EVER   integer
##                     DIS_IBS_FAM_EVER   integer
##                  DIS_ECZEMA_FAM_EVER   integer
##                     DIS_SLE_FAM_EVER   integer
##                      DIS_PS_FAM_EVER   integer
##                      DIS_MS_FAM_EVER   integer
##                      DIS_OP_FAM_EVER   integer
##               DIS_ARTHRITIS_FAM_EVER   integer
##                  DIS_CANCER_FAM_EVER   integer
##                    DIS_CANCER_F_EVER   integer
##                    DIS_CANCER_M_EVER   integer
##                  DIS_CANCER_SIB_EVER   integer
##                DIS_CANCER_CHILD_EVER   integer
##                             SLE_TIME   integer
##                         SLE_TIME_CAT   integer
##                     SLE_TROUBLE_FREQ   integer
##                        SLE_LIGHT_EXP   integer
##                      UVE_TANNING_CUR   integer
##                    UVE_SKIN_REACTION   integer
##                       UVE_TIME_WKDAY   integer
##                       UVE_TIME_WKEND   integer
##                       UVE_PROTECTION   integer
##                             UVE_HAIR   integer
##                              UVE_EYE   integer
##                          NUT_VEG_QTY   integer
##                       NUT_FRUITS_QTY   integer
##                        NUT_JUICE_QTY   integer
##                             ALC_EVER   integer
##                         ALC_CUR_FREQ   integer
##                            ALC_WKEND   integer
##                  ALC_BINGE_FREQ_MALE   integer
##                ALC_BINGE_FREQ_FEMALE   integer
##                       SMK_CIG_STATUS   integer
##                         SMK_CIG_EVER   integer
##                   SMK_CIG_WHOLE_EVER   integer
##                  SMK_CIG_WHOLE_ONSET   integer
##                     SMK_CIG_CUR_FREQ   integer
##              SMK_CIG_DAILY_CUR_ONSET   integer
##                        SMK_PATCH_CUR   integer
##                          SMK_GUM_CUR   integer
##               PSE_CHILDHOOD_DURATION   integer
##              PSE_ADULT_HOME_DURATION   integer
##               PSE_ADULT_WRK_DURATION   integer
##                        PSE_HOME_FREQ   integer
##                     PSE_LEISURE_FREQ   integer
##                         PSE_WRK_FREQ   integer
##                          PA_VIG_FREQ   integer
##                          PA_VIG_TIME   integer
##                          PA_MOD_FREQ   integer
##                          PA_MOD_TIME   integer
##                         PA_WALK_FREQ   integer
##                         PA_WALK_TIME   integer
##                   PA_TOTAL_VIG_SHORT   integer
##                   PA_TOTAL_MOD_SHORT   integer
##                  PA_TOTAL_WALK_SHORT   numeric
##                       PA_TOTAL_SHORT   numeric
##                       PA_LEVEL_SHORT   integer
##                    PA_JOB_UNPAID_WRK   integer
##                    PA_TOTAL_VIG_LONG   integer
##                    PA_TOTAL_MOD_LONG   numeric
##                   PA_TOTAL_WALK_LONG   numeric
##                        PA_TOTAL_LONG   numeric
##                        PA_LEVEL_LONG   integer
##                    PA_SIT_TIME_WKDAY   integer
##                    PA_SIT_TIME_WKEND   integer
##                    PA_TOTAL_SIT_TIME   integer
##                  PA_SIT_AVG_TIME_DAY   numeric
##                    SDC_EB_ABORIGINAL   integer
##                          SDC_EB_ARAB   integer
##                         SDC_EB_BLACK   integer
##                       SDC_EB_E_ASIAN   integer
##                      SDC_EB_FILIPINO   integer
##                        SDC_EB_JEWISH   integer
##                         SDC_EB_LATIN   integer
##                       SDC_EB_S_ASIAN   integer
##                      SDC_EB_SE_ASIAN   integer
##                       SDC_EB_W_ASIAN   integer
##                         SDC_EB_WHITE   integer
##                         SDC_EB_OTHER   integer
##                    SDC_BIRTH_COUNTRY   integer
##                      SDC_ARRIVAL_AGE   integer
##                        WRK_FULL_TIME   integer
##                        WRK_PART_TIME   integer
##                       WRK_RETIREMENT   integer
##                      WRK_HOME_FAMILY   integer
##                           WRK_UNABLE   integer
##                       WRK_UNEMPLOYED   integer
##                           WRK_UNPAID   integer
##                          WRK_STUDENT   integer
##                       WRK_EMPLOYMENT   integer
##                 WRK_IND_TYPE_CUR_CAT   integer
##                 WRK_SCHEDULE_CUR_CAT   integer
##               PM_STAND_HEIGHT_SR_AVG   numeric
##                     PM_WEIGHT_SR_AVG   numeric
##                        PM_HIP_SR_AVG   numeric
##                      PM_WAIST_SR_AVG   numeric
##                PM_WAIST_HIP_RATIO_SR   numeric
##                            PM_BMI_SR   numeric
##                        DIS_ENDO_EVER   integer
##                DIS_ENDO_HB_CHOL_EVER   integer
##                 DIS_ENDO_HB_CHOL_AGE   integer
##                  DIS_ENDO_SUGAR_EVER   integer
##                   DIS_ENDO_SUGAR_AGE   integer
##                     DIS_ENDO_TD_EVER   integer
##                      DIS_ENDO_TD_AGE   integer
##                DIS_ENDO_TD_HYPO_EVER   integer
##               DIS_ENDO_TD_HYPER_EVER   integer
##              DIS_ENDO_TD_NODULE_EVER   integer
##         DIS_ENDO_TD_THYROIDITIS_EVER   integer
##         DIS_CARDIO_PREM_HD_MALE_EVER   integer
##       DIS_CARDIO_PREM_HD_FEMALE_EVER   integer
##                      DIS_CARDIO_EVER   integer
##                  DIS_CARDIO_DVT_EVER   integer
##                   DIS_CARDIO_DVT_AGE   integer
##                   DIS_CARDIO_PE_EVER   integer
##                    DIS_CARDIO_PE_AGE   integer
##               DIS_CARDIO_ANGINA_EVER   integer
##                DIS_CARDIO_ANGINA_AGE   integer
##               DIS_CARDIO_ANGINA_LAST   integer
##                  DIS_CARDIO_TIA_EVER   integer
##                   DIS_CARDIO_TIA_AGE   integer
##                   DIS_CARDIO_HF_EVER   integer
##                    DIS_CARDIO_HF_AGE   integer
##                   DIS_CARDIO_HD_EVER   integer
##                  DIS_CARDIO_VHD_EVER   integer
##                   DIS_CARDIO_VHD_AGE   integer
##           DIS_CARDIO_VHD_AORTIC_EVER   integer
##  DIS_CARDIO_VHD_MITRAL_STENOSIS_EVER   integer
##     DIS_CARDIO_VHD_MITRAL_VALVE_EVER   integer
##        DIS_CARDIO_VHD_RHEUMATIC_EVER   integer
##            DIS_CARDIO_VHD_OTHER_EVER   integer
##                  DIS_CARDIO_CHD_EVER   integer
##                   DIS_CARDIO_CHD_AGE   integer
##                 DIS_CARDIO_PERI_EVER   integer
##                  DIS_CARDIO_PERI_AGE   integer
##               DIS_CARDIO_ATRIAL_EVER   integer
##                DIS_CARDIO_ATRIAL_AGE   integer
##      DIS_CARDIO_ATRIAL_THINNERS_EVER   integer
##                 DIS_CARDIO_ARRH_EVER   integer
##                  DIS_CARDIO_ARRH_AGE   integer
##                DIS_CARDIO_OTHER_EVER   integer
##                 DIS_CARDIO_OTHER_AGE   integer
##                        DIS_RESP_EVER   integer
##               DIS_RESP_HAYFEVER_EVER   integer
##                DIS_RESP_HAYFEVER_AGE   integer
##            DIS_RESP_SLEEP_APNEA_EVER   integer
##             DIS_RESP_SLEEP_APNEA_AGE   integer
##                  DIS_RESP_OTHER_EVER   integer
##                   DIS_RESP_OTHER_AGE   integer
##                      DIS_GASTRO_EVER   integer
##               DIS_GASTRO_ULCERS_EVER   integer
##                DIS_GASTRO_ULCERS_AGE   integer
##                 DIS_GASTRO_GERD_EVER   integer
##                  DIS_GASTRO_GERD_AGE   integer
##             DIS_GASTRO_H_PYLORI_EVER   integer
##              DIS_GASTRO_H_PYLORI_AGE   integer
##             DIS_GASTRO_BARRETTS_EVER   integer
##              DIS_GASTRO_BARRETTS_AGE   integer
##          DIS_GASTRO_INDIGESTION_EVER   integer
##           DIS_GASTRO_INDIGESTION_AGE   integer
##         DIS_GASTRO_DIVERTICULAR_EVER   integer
##          DIS_GASTRO_DIVERTICULAR_AGE   integer
##                  DIS_GASTRO_EOE_EVER   integer
##                   DIS_GASTRO_EOE_AGE   integer
##               DIS_GASTRO_CELIAC_EVER   integer
##                DIS_GASTRO_CELIAC_AGE   integer
##                       DIS_LIVER_EVER   integer
##                 DIS_LIVER_FATTY_EVER   integer
##                  DIS_LIVER_FATTY_AGE   integer
##          DIS_LIVER_PANCREATITIS_EVER   integer
##           DIS_LIVER_PANCREATITIS_AGE   integer
##            DIS_LIVER_GALLSTONES_EVER   integer
##             DIS_LIVER_GALLSTONES_AGE   integer
##                          DIS_RD_EVER   integer
##                          DIS_MH_EVER   integer
##                  DIS_MH_BIPOLAR_EVER   integer
##                   DIS_MH_BIPOLAR_AGE   integer
##                  DIS_MH_ANXIETY_EVER   integer
##                   DIS_MH_ANXIETY_AGE   integer
##                   DIS_MH_EATING_EVER   integer
##                    DIS_MH_EATING_AGE   integer
##                 DIS_MH_ANOREXIA_EVER   integer
##                  DIS_MH_BULIMIA_EVER   integer
##                DIS_MH_BINGE_EAT_EVER   integer
##                     DIS_MH_PTSD_EVER   integer
##                      DIS_MH_PTSD_AGE   integer
##            DIS_MH_SCHIZOPHRENIA_EVER   integer
##             DIS_MH_SCHIZOPHRENIA_AGE   integer
##                      DIS_MH_OCD_EVER   integer
##                       DIS_MH_OCD_AGE   integer
##                DIS_MH_ADDICTION_EVER   integer
##                 DIS_MH_ADDICTION_AGE   integer
##                       DIS_NEURO_EVER   integer
##             DIS_NEURO_PARKINSON_EVER   integer
##              DIS_NEURO_PARKINSON_AGE   integer
##              DIS_NEURO_MIGRAINE_EVER   integer
##               DIS_NEURO_MIGRAINE_AGE   integer
##                DIS_NEURO_AUTISM_EVER   integer
##                 DIS_NEURO_AUTISM_AGE   integer
##              DIS_NEURO_EPILEPSY_EVER   integer
##               DIS_NEURO_EPILEPSY_AGE   integer
##                DIS_NEURO_SPINAL_EVER   integer
##                 DIS_NEURO_SPINAL_AGE   integer
##                        DIS_BONE_EVER   integer
##                   DIS_BONE_GOUT_EVER   integer
##                    DIS_BONE_GOUT_AGE   integer
##                    DIS_BONE_CBP_EVER   integer
##                     DIS_BONE_CBP_AGE   integer
##                    DIS_BONE_CNP_EVER   integer
##                     DIS_BONE_CNP_AGE   integer
##           DIS_BONE_FIBROMYALGIA_EVER   integer
##            DIS_BONE_FIBROMYALGIA_AGE   integer
##             DIS_BONE_OSTEOPENIA_EVER   integer
##              DIS_BONE_OSTEOPENIA_AGE   integer
##                       DIS_INFEC_EVER   integer
##            DIS_INFEC_MENINGITIS_EVER   integer
##             DIS_INFEC_MENINGITIS_AGE   integer
##                   DIS_INFEC_HIV_EVER   integer
##                    DIS_INFEC_HIV_AGE   integer
##               DIS_INFEC_MALARIA_EVER   integer
##                DIS_INFEC_MALARIA_AGE   integer
##                    DIS_INFEC_TB_EVER   integer
##                     DIS_INFEC_TB_AGE   integer
##             DIS_INFEC_CHLAMYDIA_EVER   integer
##              DIS_INFEC_CHLAMYDIA_AGE   integer
##                DIS_INFEC_HERPES_EVER   integer
##                 DIS_INFEC_HERPES_AGE   integer
##             DIS_INFEC_GONORRHEA_EVER   integer
##              DIS_INFEC_GONORRHEA_AGE   integer
##              DIS_INFEC_SYPHILIS_EVER   integer
##               DIS_INFEC_SYPHILIS_AGE   integer
##                   DIS_INFEC_HPV_EVER   integer
##                    DIS_INFEC_HPV_AGE   integer
##                   DIS_INFEC_STI_EVER   integer
##                    DIS_INFEC_STI_AGE   integer
##                         DIS_GYN_EVER   integer
##                    DIS_GYN_PCOS_EVER   integer
##                     DIS_GYN_PCOS_AGE   integer
##                DIS_GYN_FIBROIDS_EVER   integer
##                 DIS_GYN_FIBROIDS_AGE   integer
##           DIS_GYN_ENDOMETRIOSIS_EVER   integer
##            DIS_GYN_ENDOMETRIOSIS_AGE   integer
##                         DIS_GEN_EVER   integer
##                      DIS_GEN_DS_EVER   logical
##                     DIS_GEN_SCA_EVER   logical
##                      DIS_GEN_SCA_AGE   integer
##             DIS_GEN_THALASSEMIA_EVER   logical
##              DIS_GEN_THALASSEMIA_AGE   integer
##                     DIS_GEN_CAH_EVER   logical
##                     DIS_GEN_AIS_EVER   logical
##                      DIS_GEN_AIS_AGE   integer
##              DIS_GEN_HEMOPHILIA_EVER   logical
##               DIS_GEN_HEMOPHILIA_AGE   integer
##                      DIS_GEN_CF_EVER   logical
##                       DIS_GEN_CF_AGE   integer
##                      DIS_GEN_KS_EVER   logical
##                       DIS_GEN_KS_AGE   integer
##                      DIS_GEN_TS_EVER   logical
##                       DIS_GEN_TS_AGE   integer
##                         DIS_EYE_EVER   integer
##                 DIS_EYE_MACULAR_EVER   integer
##                  DIS_EYE_MACULAR_AGE   integer
##                DIS_EYE_GLAUCOMA_EVER   integer
##                 DIS_EYE_GLAUCOMA_AGE   integer
##               DIS_EYE_CATARACTS_EVER   integer
##                DIS_EYE_CATARACTS_AGE   integer
##                DIS_EYE_DIAB_RET_EVER   integer
##                 DIS_EYE_DIAB_RET_AGE   integer
##                         DIS_EAR_EVER   integer
##                DIS_EAR_TINNITUS_EVER   integer
##                 DIS_EAR_TINNITUS_AGE   integer
##                 DIS_EAR_TINNITUS_DUR   integer
##                DIS_EAR_TINNITUS_FREQ   integer
##              DIS_EAR_TINNITUS_NATURE   integer
##              DIS_EAR_TINNITUS_AFFECT   integer
##                    DIS_EAR_LOSS_EVER   integer
##                     DIS_EAR_LOSS_AGE   integer
##                             ALE06_06   numeric
##                             ALE06_07   integer
##                             ALE16_06   numeric
##                             ALE16_07   numeric
##                          MSD11_DAPOP   integer
##                             MSD11_PR character
##                            MSD11_REG character
##                           MSD11_ZONE character
##                            MSD11_CMA character
##                            MSD11_MFS   numeric
##                            MSD11_SFS   numeric
##                           GRLAN10_09   numeric
##                        NO2LUR06_A_01   numeric
##                       NO2LUR08_RA_01   numeric
##                           O3CHG15_01   numeric
##                         PM25DAL12_01   numeric
##                          SO2OMI12_01   numeric
##                          WTHNRC15_01   numeric
##                          WTHNRC15_02   numeric
##                          WTHNRC15_03   numeric
##                          WTHNRC15_04   numeric
##                          WTHNRC15_05   numeric
##                          WTHNRC15_07   numeric
##                          WTHNRC15_08   integer
##                          WTHNRC15_09   integer
##                          WTHNRC15_10   numeric
##                          WTHNRC15_11   numeric
##                          WTHNRC15_12   numeric
##                          WTHNRC15_13   integer
##                          WTHNRC15_14   integer
##                          WTHNRC15_15   numeric
##                          WTHNRC15_16   numeric
##                          WTHNRC15_17   integer
##                          WTHNRC15_18   integer
##                          WTHNRC15_19   numeric
##                          LGTNLT12_01   integer
```

In this health administrative dataset, there are 41,187 observations and 440 variables. Most of these variables are integers, numeric, or character, which makes sense. However, some variables are being treated as logical. Let’s identify those logical variables.


``` r
data %>% 
  select_if(is_logical) %>% 
  glimpse()
```

```
## Rows: 41,187
## Columns: 9
## $ DIS_GEN_DS_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_SCA_EVER         <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_THALASSEMIA_EVER <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_CAH_EVER         <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_AIS_EVER         <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_HEMOPHILIA_EVER  <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_CF_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_KS_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_TS_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
```


We have 9 variables that are logical so let's drop those.



``` r
### Select specific columns
logical_cols <- c("DIS_GEN_DS_EVER", "DIS_GEN_SCA_EVER", "DIS_GEN_THALASSEMIA_EVER", "DIS_GEN_CAH_EVER", "DIS_GEN_AIS_EVER", "DIS_GEN_HEMOPHILIA_EVER", "DIS_GEN_CF_EVER", "DIS_GEN_KS_EVER", "DIS_GEN_TS_EVER")

data <- data %>% select(!(logical_cols))
```

```
## Warning: Using an external vector in selections was deprecated in tidyselect 1.1.0.
## ℹ Please use `all_of()` or `any_of()` instead.
##   # Was:
##   data %>% select(logical_cols)
## 
##   # Now:
##   data %>% select(all_of(logical_cols))
## 
## See <https://tidyselect.r-lib.org/reference/faq-external-vector.html>.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
```
**Identify Missing Data**



``` r
missing_table <- miss_var_summary(data)
missing_table
```

```
## # A tibble: 431 × 3
##    variable                       n_miss pct_miss
##    <chr>                           <int>    <num>
##  1 DIS_CARDIO_PREM_HD_FEMALE_EVER  41081     99.7
##  2 DIS_CARDIO_PREM_HD_MALE_EVER    41061     99.7
##  3 DIS_MH_BIPOLAR_EVER             40914     99.3
##  4 DIS_EAR_TINNITUS_NATURE         40880     99.3
##  5 DIS_ENDO_TD_AGE                 40862     99.2
##  6 DIS_ENDO_SUGAR_AGE              40861     99.2
##  7 DIS_RESP_OTHER_EVER             40858     99.2
##  8 DIS_MH_EATING_EVER              40857     99.2
##  9 DIS_LIVER_FATTY_EVER            40856     99.2
## 10 DIS_EAR_TINNITUS_FREQ           40854     99.2
## # ℹ 421 more rows
```
Although the proportion of missing data can influence statistical inference, there are no universally accepted guidelines for the maximum amount of missing data for which multiple imputation (MI) remains beneficial. One study suggests that when over 10% of data are missing, the estimates may become biased [@bennett2001can]. Another paper proposes 5% as a threshold, below which MI is unlikely to provide significant benefits [@schafer1999multiple]. However, limited evidence exists to support these cutoff points. Few studies have explored how bias and efficiency change with increasing levels of missing data, with the most extreme case being 50% missing data, which showed growing inconsistency in effect estimates as missingness increased [@mishra2014comparative] for the small sample. However, when both high missing data and large sample sizes are considered as missing data being at random (MAR) [@lee2012recovery]. In this analysis, I consider missing values with less than 50 percent in this dataset.

let's review filter out all variables with more than 50% missing.



``` r
data <- data %>%
          select(where(~sum(is.na(.x))/length(.x) < 0.80))

missing_table <- miss_var_summary(data)
```

``` r
missing_table <- miss_var_summary(data)
missing_table
```

```
## # A tibble: 247 × 3
##    variable                  n_miss pct_miss
##    <chr>                      <int>    <num>
##  1 SMK_CIG_WHOLE_ONSET        32020     77.7
##  2 DIS_ARTHRITIS_TYPE2        29704     72.1
##  3 MSD11_CMA                  29574     71.8
##  4 DIS_ARTHRITIS_TYPE3        29126     70.7
##  5 DIS_CARDIO_HD_EVER         24566     59.6
##  6 DIS_RESP_SLEEP_APNEA_AGE   23938     58.1
##  7 DIS_NEURO_MIGRAINE_AGE     23786     57.8
##  8 DIS_ENDO_HB_CHOL_AGE       23625     57.4
##  9 DIS_MH_ANXIETY_AGE         23334     56.7
## 10 DIS_RESP_SLEEP_APNEA_EVER  23308     56.6
## # ℹ 237 more rows
```

### Summarize findings using tables, charts, or heatmaps to visualize missingness. 


``` r
gg_miss_upset(data, order.by = "freq", nsets = 10)
```

![](Missing-Data_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

Suppose we want to make mode where 
We have identified the outcome and predictors variable. Follwoing are the outcoma and predictor variables.

## Main Outcome of Interest: 

BMI: Body Mass Index (PM_BMI_SR).

## Expouser

PA: Physical Activities: PA_TOTAL_SHORT

SL: Sedentary lifestyle: Total sitting time per week:PA_TOTAL_SIT_TIME 

## Predictors:

### Social and demographic factor:

EB: Participant's ethnic background is Aboriginal (e.g. First Nations, Metis, Inuit).:SDC_EB_ABORIGINAL

AGE: Age of the respondent: SDC_AGE_CALC

GE: Gender: SDC_GENDER

ES: Employment Status: WRK_EMPLOYMENT

GPH: General perception of health: HS_GEN_HEALTH

FI: Food Intake: NUT_VEG_QTY, NUT_FRUITS_QTY

SM: Smoking status: SMK_CIG_STATUS

AC: Alcohol consumption: ALC_CUR_FREQ

### Phychological factor:

DE: Depression: DIS_DEP_EVER

### Choronic health condition 

DIA: Diabetes: DIS_DIAB_TYPE


### Enviromental factor:


RE: Region: ADM_STUDY_ID

``` r
working_data<- data %>%
  select(ID, PM_BMI_SR, PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME , SDC_EB_ABORIGINAL, SDC_AGE_CALC, SDC_GENDER, WRK_EMPLOYMENT, HS_GEN_HEALTH, NUT_VEG_QTY, NUT_FRUITS_QTY, SMK_CIG_STATUS, ALC_CUR_FREQ, DIS_DEP_EVER, DIS_DIAB_TYPE , ADM_STUDY_ID)
```



<!-- 2. **Apply Imputation Methods**   -->
<!--    - Select and apply at least three different methods for imputing missing data, such as:   -->
<!--      - Mean/Median/Mode imputation. -->
<!-- Lets apply mice function to impute missing data by mean imputation. Here, we have select 1 imputation and 1 iteration.  -->
<!-- ```{r} -->
<!-- set.seed(123) -->
<!-- data_imp_mean <- mice(data, method = "mean", m = 1, maxit = 1) -->
<!-- data_mean_c <- complete(data_imp_mean) -->
<!-- ``` -->

<!--      - K-Nearest Neighbors (KNN) imputation.  -->

<!-- KNN imputation replaces missing values based on the values of the nearest neighbors. -->

<!-- Implementation: -->
<!-- ```{r} -->
<!-- set.seed(456) -->
<!-- imputed_data_KNN <- kNN(data, k = 3)  # k = number of nearest neighbors -->
<!-- ``` -->

<!--      - Multiple Imputation by Chained Equations (MICE).  -->
<!--      MICE is a robust method for handling missing data by creating multiple imputed datasets and combining the results. Here we consider 5 imputation (according to theory this sould be more thanb 20 ) and 5 number of iteration -->
<!-- ```{r} -->
<!-- imputed_data_mice <- mice(data, m = 5, seed = 567, maxit=5) -->
<!-- imputed_data_mice_c<-complete(imputed_data_mice) -->
<!-- ``` -->
<!--    - Document the implementation process for each method.  -->

<!-- 3. **Evaluation of Imputation Methods**   -->
<!--    - Compare the imputed datasets by analyzing:   -->
<!--      - Changes in key summary statistics (e.g., means, variances).   -->
<!--      - The preservation of relationships between variables (e.g., correlations).   -->
<!--      - Visual comparisons of distributions before and after imputation.  -->
<!-- 4. **Analysis of Imputed Data**   -->
<!--    - Conduct a simple statistical analysis on the imputed datasets to illustrate the downstream effects of different imputation methods.   -->
<!--    - Discuss how the choice of imputation method impacts the analysis results.   -->

<!-- 5. **Interpretation and Reporting**   -->
<!--    - Provide a detailed comparison of the methods, discussing their strengths, weaknesses, and suitability for the dataset.   -->
<!--    - Reflect on the challenges of handling missing data in health research.   -->


<!-- ## References -->
