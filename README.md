# Abstract
In recent times, much software MNCs have implemented facial recognition software for services like surveillance, photo-tagging, maintaining identity records etc. So, the question has arisen whether our identity is safe from leaks of sensitive data and are the companies following proper safety guidelines. Image recognition has become an integral part of many organization’s operations such as Facebook implementing tagging people in uploaded pics, government installing surveillance cameras, CCTV cameras in banks and other institutions, etc. Thus, there is a need to protect this info from untrusted sources by privatizing the data. With this comes the need of preventing hackers/adversaries from accessing sensitive information. In this project, our aim is to implement one such method of anonymizing facial images using deidentification techniques.

# Introduction
In an age of widespread data collecting and sharing, the safeguarding of people’s sensitive information has become critical. Facial photos and tabular data frequently contain personal information that, if revealed, can lead to identity theft, discrimination, and other types of harm. This study is driven by the urgent need to create effective de-identification algorithms that might limit these hazards while enabling the responsible use of data for research, AI applications, and collaborative analysis. This research intends to adopt L-diversity not only to fulfill legislative requirements but also to sustain ethical norms, retain public confidence, and strike a balance between data value and privacy. Ultimately, the goal is to enable enterprises to reap the benefits of data-driven insights while preserving individuals' privacy rights in an increasingly linked world

# Project Outcome
There are many methods available to implement de-identification of facial images such as blurring out the image, hiding certain facial features or modifying the facial features by adding some noise, calculated by taking out average values of certain facial features such as skincolor, shape etc. SAP HANA Cloud, which provides a safe and scalable platform for storing and retrieving massive volumes of data, may be utilized to store and manage these anonymized photos, which we would be implementing in this project

# Proposed Methadology
The paper introduces a pioneering algorithm designed to enhance the anonymization of medical records, with a particular focus on preserving data utility in the context of DICOM (Digital Imaging and Communications in Medicine) format records. Our approach builds upon the wellestablished foundation of k-anonymity by incorporating the innovative concept of l-diversity. This amalgamation addresses a critical limitation of traditional k- anonymity, where individual records can still be vulnerable to attribute disclosure. By leveraging l-diversity, our algorithm ensures that within each equivalence class of k-anonymous records, there is a diversified representation of sensitive attributes, thereby fortifying the protection of patient identities.

Notably, the novelty of our improved algorithm lies in its adaptability to the complex and multifaceted nature of DICOM data, which encompasses both graphical image information and tabular data containing identifying details. This unique feature facilitates comprehensive anonymization, rendering the algorithm highly effective in safeguarding patient privacy while simultaneously optimizing the utility of the anonymized data for research purposes. Researchers can confidently utilize the anonymized DICOM records, knowing that the risk of attribute disclosure has been significantly mitigated, thus unlocking new opportunities for valuable medical research without compromising patient confidentiality.

# Architecture

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/4914f3a6-bea4-4be4-9b13-525cadb344ec)

# Results 
The dataset used to depict the computations of the anonymization process is a modified version of the PHI information embedded in the DICOM images of the open-acces Stanford CheXNet database (source). This dataset contains 15,060 rows, each having attributes like Patient ID, Age, SSN, Marital status, Gender, Ethnicity, Race, address, and so on. Of course, primary identifiers like Patient ID and SSN have been redacted in the publicly available version; these are not of importance, since only quasi-identifiers are being dealt with by our algorithm. After making sure that the dataset is parsed properly, we collect the attribute classification information, which tells the tool which all attributes are direct, quasi, sensitive and insensitive.

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/8d716a9b-2e29-475c-ab7f-17a8e357b92b)

The dataset has 3052 unique combinations of quasi-identifier values and the y-axis represents how many records are there in each of these equivalent classes. For a very common set of quasiidentifier sets (like., “(20, <address>, ‘Never-married’, ‘Female’)”) one can see that there are a lot of records in that specific equivalent class. The first step in the anonymization process is the suppression of direct-identifiers.

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/6cc82aea-e2aa-4095-9c47-692b5f7f0aaa)

The next steps contain the Mondrian algorithm trying to partition the entire dataset into equivalent classes (size ≥ k) each satisfying the l-diversity and t-closeness parameters. Once the required partitions are obtained, we proceed to the generalization process where the quasiidentifying attributes in each of these equivalent classes are generalized to make it satisfy kanonymity.

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/15bd6aa8-bc22-49af-9523-af0b2921a82d)

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/9ebdee89-20e9-43a8-9428-953f525cd5ba)

The resulting dataset was analysed using the previously defined utility measures. The output of our prototype is shown below. The following changes in metrics were observed.

• Generalization Information Loss (GenILoss) is usually within the range 0 (no transformation) to 1 (full suppression). The anonymized dataset is having the value 0.33. Thus, the dataset is generalized as required without much loss in information.

• Discernibility Metric (DM) of the dataset before and after anonymization is measures. Before anonymization it was 2,137,444 and after anonymization it is 98,510. Thus we can see a twenty-fold or 20× decrease in value; i.e., more equivalent classes now have their size under k.

• Average Equivalence Class Size Metric before anonymization had a value of 0.022 and after anonymization, the value is 1.413. Although the ideal value is 1, 1.413 is closer to 1 than 0.120. Hence, we can observe a significant improvement. The results of the anonymization algorithm described previously have been examined on an exemplar set of facial images — the UTK-Face* dataset, available for open access.

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/a5e090ea-529d-4957-b6c2-8bd1b1e9d7d5)
![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/90fd3ecf-cfc6-4f30-8928-3fcbceb07597)


It is to be noted, however, that the utility of the image is preserved. Faces have been taken as exemplar samples in this example, but the principle may be extended to any other graphic content of electronic health records — including, but not limited to, tomographic scans, resonance imaging, other radiological images of skeletal structures, lungs, and other parts of the body. Further, the results for the anonymization of the tabular data present in the DICOM images is shown below.

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/a62ae57c-6b04-4a77-af97-5d527e044899)

# Conclusion
This project presents a comprehensive architecture that effectively addresses the pressing concerns surrounding data privacy while retaining the data's analytical utility. The architecture encompasses key stages, from data collection and preprocessing to advanced de-identification techniques for both facial images and tabular data. It ensures that the resulting data is both privacy-compliant and secure, complete with stringent access controls and auditing mechanisms. Striking a balance between safeguarding individual privacy and facilitating meaningful data analysis, this architecture empowers organizations to extract valuable insights from their data without compromising personal privacy.

Looking ahead, its future scope includes the integration of advanced privacy techniques, real-time monitoring, machine learning applications, and adaptability to evolving global data privacy regulations. It is expected to continue evolving to handle large volumes of data while offering user-friendly interfaces and tailored solutions for specific industries, cementing its relevance in a world where data privacy and analytics are of paramount importance.

# Future Scope
The scope of this paper merely covers utility preservation from a statistical perspective. Future works could improve the visual fidelity of anonymized images specifically for AI-based diagnostic tools, ensuring that these tools can extract maximum value from the data without compromising privacy. Additionally, this algorithm may also not work well in real-time applications like telemedicine and emergency care; further exploration can be done in reducing the latency of anonymization.

# Contributors

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/429ac004-f519-4a3a-901e-8843a1fde2f7)

# Poster

![image](https://github.com/KasiR07/Anonymizing-Medical-Records-using-K-Anonymity-and-L-Diversity/assets/108777263/a65a23b2-0830-42c5-92a8-48ab076f5bc6)


