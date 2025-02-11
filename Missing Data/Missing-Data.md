---
title: "Missing Data"
author: "Syed Jafar Raza Rizvi <br> NSID: cfr954 <br> Student ID: 11344782"
output:
  html_document:
    keep_md: true
date: "2025-02-11"
bibliography: scholar.bib
---


# 1. **Dataset Exploration**  
   - Load the provided health administrative dataset.  
   - Explore the dataset to identify the extent, patterns, and potential reasons for missing data.  
   - Summarize findings using tables, charts, or heatmaps to visualize missingness.  
   
## - Load the provided health administrative dataset.

``` r
data<-read.csv("can_path_data.csv")
data <- data %>% select(ID:HS_GEN_HEALTH, PA_TOTAL_SHORT, PM_BMI_SR, contains("_EVER"), contains("WRK_"))
```

## - Explore the dataset to identify the extent, patterns, and potential reasons for missing data.

### Explore Dataset 

**Check the structure of the dataset**


``` r
dim(data)
```

```
## [1] 41187   195
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
##                       PA_TOTAL_SHORT   numeric
##                            PM_BMI_SR   numeric
##                HS_ROUTINE_VISIT_EVER   integer
##                 HS_DENTAL_VISIT_EVER   integer
##                         HS_FOBT_EVER   integer
##                          HS_COL_EVER   integer
##                          HS_SIG_EVER   integer
##                      HS_SIG_COL_EVER   integer
##                        HS_POLYP_EVER   integer
##                          HS_PSA_EVER   integer
##               WH_CONTRACEPTIVES_EVER   integer
##                          WH_HFT_EVER   integer
##                    WH_MENOPAUSE_EVER   integer
##                          WH_HRT_EVER   integer
##                 WH_HYSTERECTOMY_EVER   integer
##                 WH_OOPHORECTOMY_EVER   integer
##                          HS_MMG_EVER   integer
##                          HS_PAP_EVER   integer
##                         DIS_HBP_EVER   integer
##                          DIS_MI_EVER   integer
##                      DIS_STROKE_EVER   integer
##                      DIS_ASTHMA_EVER   integer
##                   DIS_EMPHYSEMA_EVER   integer
##                          DIS_CB_EVER   integer
##                        DIS_COPD_EVER   integer
##                         DIS_DEP_EVER   integer
##                        DIS_DIAB_EVER   integer
##                          DIS_LC_EVER   integer
##                          DIS_CH_EVER   integer
##                       DIS_CROHN_EVER   integer
##                          DIS_UC_EVER   integer
##                         DIS_IBS_EVER   integer
##                      DIS_ECZEMA_EVER   integer
##                         DIS_SLE_EVER   integer
##                          DIS_PS_EVER   integer
##                          DIS_MS_EVER   integer
##                          DIS_OP_EVER   integer
##                   DIS_ARTHRITIS_EVER   integer
##                      DIS_CANCER_EVER   integer
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
##                             ALC_EVER   integer
##                         SMK_CIG_EVER   integer
##                   SMK_CIG_WHOLE_EVER   integer
##                        DIS_ENDO_EVER   integer
##                DIS_ENDO_HB_CHOL_EVER   integer
##                  DIS_ENDO_SUGAR_EVER   integer
##                     DIS_ENDO_TD_EVER   integer
##                DIS_ENDO_TD_HYPO_EVER   integer
##               DIS_ENDO_TD_HYPER_EVER   integer
##              DIS_ENDO_TD_NODULE_EVER   integer
##         DIS_ENDO_TD_THYROIDITIS_EVER   integer
##         DIS_CARDIO_PREM_HD_MALE_EVER   integer
##       DIS_CARDIO_PREM_HD_FEMALE_EVER   integer
##                      DIS_CARDIO_EVER   integer
##                  DIS_CARDIO_DVT_EVER   integer
##                   DIS_CARDIO_PE_EVER   integer
##               DIS_CARDIO_ANGINA_EVER   integer
##                  DIS_CARDIO_TIA_EVER   integer
##                   DIS_CARDIO_HF_EVER   integer
##                   DIS_CARDIO_HD_EVER   integer
##                  DIS_CARDIO_VHD_EVER   integer
##           DIS_CARDIO_VHD_AORTIC_EVER   integer
##  DIS_CARDIO_VHD_MITRAL_STENOSIS_EVER   integer
##     DIS_CARDIO_VHD_MITRAL_VALVE_EVER   integer
##        DIS_CARDIO_VHD_RHEUMATIC_EVER   integer
##            DIS_CARDIO_VHD_OTHER_EVER   integer
##                  DIS_CARDIO_CHD_EVER   integer
##                 DIS_CARDIO_PERI_EVER   integer
##               DIS_CARDIO_ATRIAL_EVER   integer
##      DIS_CARDIO_ATRIAL_THINNERS_EVER   integer
##                 DIS_CARDIO_ARRH_EVER   integer
##                DIS_CARDIO_OTHER_EVER   integer
##                        DIS_RESP_EVER   integer
##               DIS_RESP_HAYFEVER_EVER   integer
##            DIS_RESP_SLEEP_APNEA_EVER   integer
##                  DIS_RESP_OTHER_EVER   integer
##                      DIS_GASTRO_EVER   integer
##               DIS_GASTRO_ULCERS_EVER   integer
##                 DIS_GASTRO_GERD_EVER   integer
##             DIS_GASTRO_H_PYLORI_EVER   integer
##             DIS_GASTRO_BARRETTS_EVER   integer
##          DIS_GASTRO_INDIGESTION_EVER   integer
##         DIS_GASTRO_DIVERTICULAR_EVER   integer
##                  DIS_GASTRO_EOE_EVER   integer
##               DIS_GASTRO_CELIAC_EVER   integer
##                       DIS_LIVER_EVER   integer
##                 DIS_LIVER_FATTY_EVER   integer
##          DIS_LIVER_PANCREATITIS_EVER   integer
##            DIS_LIVER_GALLSTONES_EVER   integer
##                          DIS_RD_EVER   integer
##                          DIS_MH_EVER   integer
##                  DIS_MH_BIPOLAR_EVER   integer
##                  DIS_MH_ANXIETY_EVER   integer
##                   DIS_MH_EATING_EVER   integer
##                 DIS_MH_ANOREXIA_EVER   integer
##                  DIS_MH_BULIMIA_EVER   integer
##                DIS_MH_BINGE_EAT_EVER   integer
##                     DIS_MH_PTSD_EVER   integer
##            DIS_MH_SCHIZOPHRENIA_EVER   integer
##                      DIS_MH_OCD_EVER   integer
##                DIS_MH_ADDICTION_EVER   integer
##                       DIS_NEURO_EVER   integer
##             DIS_NEURO_PARKINSON_EVER   integer
##              DIS_NEURO_MIGRAINE_EVER   integer
##                DIS_NEURO_AUTISM_EVER   integer
##              DIS_NEURO_EPILEPSY_EVER   integer
##                DIS_NEURO_SPINAL_EVER   integer
##                        DIS_BONE_EVER   integer
##                   DIS_BONE_GOUT_EVER   integer
##                    DIS_BONE_CBP_EVER   integer
##                    DIS_BONE_CNP_EVER   integer
##           DIS_BONE_FIBROMYALGIA_EVER   integer
##             DIS_BONE_OSTEOPENIA_EVER   integer
##                       DIS_INFEC_EVER   integer
##            DIS_INFEC_MENINGITIS_EVER   integer
##                   DIS_INFEC_HIV_EVER   integer
##               DIS_INFEC_MALARIA_EVER   integer
##                    DIS_INFEC_TB_EVER   integer
##             DIS_INFEC_CHLAMYDIA_EVER   integer
##                DIS_INFEC_HERPES_EVER   integer
##             DIS_INFEC_GONORRHEA_EVER   integer
##              DIS_INFEC_SYPHILIS_EVER   integer
##                   DIS_INFEC_HPV_EVER   integer
##                   DIS_INFEC_STI_EVER   integer
##                         DIS_GYN_EVER   integer
##                    DIS_GYN_PCOS_EVER   integer
##                DIS_GYN_FIBROIDS_EVER   integer
##           DIS_GYN_ENDOMETRIOSIS_EVER   integer
##                         DIS_GEN_EVER   integer
##                      DIS_GEN_DS_EVER   logical
##                     DIS_GEN_SCA_EVER   logical
##             DIS_GEN_THALASSEMIA_EVER   logical
##                     DIS_GEN_CAH_EVER   logical
##                     DIS_GEN_AIS_EVER   logical
##              DIS_GEN_HEMOPHILIA_EVER   logical
##                      DIS_GEN_CF_EVER   logical
##                      DIS_GEN_KS_EVER   logical
##                      DIS_GEN_TS_EVER   logical
##                         DIS_EYE_EVER   integer
##                 DIS_EYE_MACULAR_EVER   integer
##                DIS_EYE_GLAUCOMA_EVER   integer
##               DIS_EYE_CATARACTS_EVER   integer
##                DIS_EYE_DIAB_RET_EVER   integer
##                         DIS_EAR_EVER   integer
##                DIS_EAR_TINNITUS_EVER   integer
##                    DIS_EAR_LOSS_EVER   integer
##               PSE_ADULT_WRK_DURATION   integer
##                         PSE_WRK_FREQ   integer
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
## # A tibble: 186 × 3
##    variable                       n_miss pct_miss
##    <chr>                           <int>    <num>
##  1 DIS_CARDIO_PREM_HD_FEMALE_EVER  41081     99.7
##  2 DIS_CARDIO_PREM_HD_MALE_EVER    41061     99.7
##  3 DIS_MH_BIPOLAR_EVER             40914     99.3
##  4 DIS_RESP_OTHER_EVER             40858     99.2
##  5 DIS_MH_EATING_EVER              40857     99.2
##  6 DIS_LIVER_FATTY_EVER            40856     99.2
##  7 DIS_MH_SCHIZOPHRENIA_EVER       40853     99.2
##  8 DIS_ENDO_SUGAR_EVER             40850     99.2
##  9 DIS_ENDO_TD_EVER                40850     99.2
## 10 DIS_GASTRO_ULCERS_EVER          40821     99.1
## # ℹ 176 more rows
```
Although the proportion of missing data can influence statistical inference, there are no universally accepted guidelines for the maximum amount of missing data for which multiple imputation (MI) remains beneficial. One study suggests that when over 10% of data are missing, the estimates may become biased [@bennett2001can]. Another paper proposes 5% as a threshold, below which MI is unlikely to provide significant benefits [@schafer1999multiple]. However, limited evidence exists to support these cutoff points. Few studies have explored how bias and efficiency change with increasing levels of missing data, with the most extreme case being 50% missing data, which showed growing inconsistency in effect estimates as missingness increased [@mishra2014comparative] for the small sample. However, when both high missing data and large sample sizes are considered as missing data being at random (MAR) [@lee2012recovery]. In this analysis, I consider missing values with less than 50 percent in this dataset.

let's review filter out all variables with more than 75% missing.



``` r
data <- data %>%
          select(where(~sum(is.na(.x))/length(.x) < 0.50))

missing_table <- miss_var_summary(data)
```

``` r
missing_table <- miss_var_summary(data)
missing_table
```

```
## # A tibble: 87 × 3
##    variable              n_miss pct_miss
##    <chr>                  <int>    <num>
##  1 HS_PAP_EVER            16182     39.3
##  2 HS_MMG_EVER            15995     38.8
##  3 PM_BMI_SR              11976     29.1
##  4 DIS_IBS_FAM_EVER       10867     26.4
##  5 DIS_CANCER_CHILD_EVER  10622     25.8
##  6 DIS_LC_FAM_EVER        10579     25.7
##  7 DIS_UC_FAM_EVER        10505     25.5
##  8 DIS_OP_FAM_EVER        10282     25.0
##  9 DIS_CH_FAM_EVER        10242     24.9
## 10 DIS_PS_FAM_EVER        10150     24.6
## # ℹ 77 more rows
```

### Summarize findings using tables, charts, or heatmaps to visualize missingness. 


``` r
gg_miss_upset(data, order.by = "freq", nsets = 10)
```

![](Missing-Data_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

## References
