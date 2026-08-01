Case Study: License Plate Detection & Blurring using YOLOv8
--
Problem statement: With the growing use of cameras in traffic monitoring and surveillance, capturing vehicle images often leads to exposure of sensitive information such as license plate numbers. This raises serious privacy and data protection concerns. The objective of this project is to build an automated system using YOLOv8 to accurately detect vehicle license plates in images or video streams and blur them in real time, ensuring privacy preservation while maintaining the usefulness of the visual data for analysis and monitoring purposes.

**Dataset link**: https://drive.google.com/drive/folders/12XiCTBw-NxoMLR4SGQVvgKBTxzWsTlXJ?usp=sharing

**Dataset description**: [data description](https://docs.google.com/document/d/1YMB6wK2OLELn4mLYvir5_S4idTEDOx6TXD3KryI1l9o/edit?tab=t.0)

**Approach document**: Refer to the document below to help guide you in solving the questions.

https://docs.google.com/document/d/1zejcjOC61YsjRA-f0r3LQaMM9ps1bl-RkZulGrSOqyM/edit?tab=t.0

Business questions:
--
1. How do you convert normalized YOLO bounding box coordinates (center_x, center_y, width, height) into pixel coordinates suitable for drawing rectangles with OpenCV?
2. Write a function to overlay bounding boxes onto raw images.
3. Why is this step critical before starting the training process?
4. How did annotation quality impact the final blurring accuracy?
5. How did you preprocess images before feeding them into YOLOv8 without losing fine-grained plate details?
6. Why did you choose YOLOv8 for license plate detection instead of a two-stage detector?
7. Which YOLOv8 variant did you select, and how did it balance speed and accuracy for this use case?
8. How did license plate characteristics influence your choice of model scale?
9. How did you apply blurring only within the detected bounding box?

Submission Criteria
--
 - File Format: Only PDF files are allowed for submission.
 - File Size Limit: The PDF must be less than 20MB in size.
 - For Google Collab Users:
    - To submit your Colab work, download it as a PDF by navigating to File > Print > Save as PDF before uploading.
    - Please note: Submitting a PDF containing a Colablink is not accepted and your submission will not be accepted
 - For Text-Based Submissions:
    - Use Google Docs or MS Word to create the document
    - Save it as a PDF before submitting
 - Single Submission Policy: Only one submission is allowed per user.
 - Please ensure that the submission pdf must not exceed 50 pages.

Evaluation Criteria
--
1. **Business Story & Context**: Clarity, relevance, and completeness of the problem narrative.
2. **Coordinate Transformation**: Accuracy of the logic used to convert normalized YOLO coordinates back into pixel-based coordinates for OpenCV processing.
3. **EDA & Analytical Logic**: Appropriateness of exploratory methods, choice of metrics, and correctness of calculations.
4. **Visualizations**: Quality, readability, and relevance of plots; effective use of visuals to illustrate findings.
5. **Insights & Recommendations**: Depth, originality, and business impact of conclusions and suggested actions.
6. **Notebook Clarity & Reproducibility**: Logical flow, clarity of explanations, clean code structure, and ease of reproducing results directly from the notebook.

Note:
--
- No edits will be allowed once you submit your file.
- Please review carefully and submit only the final version.
- Re-submission requests via support will not be accepted.