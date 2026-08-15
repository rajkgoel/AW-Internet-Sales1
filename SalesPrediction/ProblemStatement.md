# Predicting Sales from Campaign Data

## Problem Statement

Marketing teams often invest heavily in influencer campaigns, paying creators to promote products on social media platforms like Instagram. Understanding which factors actually drive product sales is critical to making better decisions about:

- who to work with,
- how much to spend, and
- how to design content.

The goal is to build a predictive model that can estimate how many units of a product will be sold based on key influencer campaign attributes.

## Dataset Link

https://drive.google.com/drive/folders/1BCTayfVYwapGcGl3Mizik1E6-zPcQ_DT?usp=sharing

## Dataset Overview

The dataset contains historical data from multiple influencer campaigns. It includes features such as:

- **Followers**: Number of Instagram followers the influencer had at the time of the campaign
- **EngagementRate (%)**: Engagement rate on posts (likes/comments per follower)
- **AdSpend (GBP)**: Total money spent on the campaign
- **ContentQuality**: Subjective score (1-10) reflecting the quality of the influencer's content
- **Sales (Units)**: Number of product units sold as a result of the campaign (target variable)
- **Timestamp**: The day the campaign ended

Additional columns such as **Timestamp** and **Notes** are also included.

## Approach Document

https://docs.google.com/document/d/1BG9fACg-wZtZCimqDR-O7Fdw0P525JXHRb6y45UFBW8/edit?usp=sharing

## Data Quality Notes

The dataset is intentionally messy and contains:

- Missing values
- Inconsistent formats (e.g., "£5000", "3.2%")
- Outliers (e.g., billions of followers, negative spend)
- Mixed scales (some follower counts are in thousands)

This reflects a realistic scenario where data was pulled together quickly from different sources.

## Provided Datasets

- **messy_train_data.csv**: Training set to clean and use for model fitting
- **messy_test_data.csv**: Test set to clean and generate predictions

## Suggested Steps

- Clean the data
- Explore and visualize relationships
- Engineer better features (e.g., log transforms, interactions)
- Train a regression model
- Perform hyperparameter tuning and cross-validation to build a robust model
- Evaluate using metrics like RMSE and R²

## Success Criteria

- A model with good predictive accuracy (high R², low RMSE)
- Clear insights into which factors matter most for driving sales
- A pipeline (a simple function) that can reliably handle future messy campaign data

## Submission Criteria

- **File format**: Only PDF files are allowed for submission.
- **File size limit**: The PDF must be less than 20 MB.
- **Single submission policy**: Only one submission is allowed per user.
- **Page limit**: The submission PDF must not exceed 50 pages.

### For Google Colab Users

- Download your Colab work as a PDF using: **File > Print > Save as PDF**.
- Submitting a PDF containing only a Colab link is not accepted.

### For Text-Based Submissions

- Use Google Docs or MS Word to create the document.
- Save it as a PDF before submitting.

## Important Notes

- No edits are allowed once you submit your file.
- Review carefully and submit only the final version.
- Re-submission requests via support will not be accepted.