
# Q-HEALTH GUARD
Team: Epic Engineers
Event: Qiskit Fall Fest 2026
Problem Statement ID: VNQFF-02
Overview
Q-HEALTH GUARD is a prototype exploring privacy-aware healthcare machine learning with an experimental quantum-kernel classification component. The project uses a synthetic healthcare dataset to demonstrate data preparation, quantum feature encoding, quantum-kernel classification, and model evaluation.
Important: This is an experimental educational prototype, not a clinical diagnostic system. Results from synthetic data are not clinical evidence, and the project does not establish quantum advantage.

Problem
Healthcare AI models may benefit from learning patterns across multiple institutions, but sharing raw patient records can create privacy and governance risks. A privacy-aware design aims to keep records local and share only approved information under explicit safeguards.
Proposed Approach
The intended high-level workflow is:
1. Prepare and validate the synthetic dataset.
2. Select a small set of numerical features and scale them.
3. Encode the features with a Qiskit quantum feature map.
4. Use FidelityQuantumKernel to calculate similarities between encoded samples.
5. Use QSVC to classify the target labels.
6. Evaluate the results and compare them with a classical SVM baseline.
7. Treat federated learning, differential privacy, and secure aggregation as separate components that require their own implementations and validation.
Quantum Component
The Qiskit experiment uses:
- Qubits: Four qubits for the four selected numerical features in the starter example.
- Feature map: ZZFeatureMap (the zz_feature_map helper in code).
- Quantum kernel: FidelityQuantumKernel.
- Classifier: QSVC.
- Baseline: A classical support-vector classifier with an RBF kernel.
The quantum-kernel classifier does not automatically implement federated learning. A kernel-based QSVC does not naturally provide shared model weights for standard FedAvg aggregation.
Dataset
Expected dataset filename:
synthetic_privacy_preserving_health_dataset.csv
The starter implementation expects these columns:
- consent_for_research
- diagnosis_label
- age_years
- bmi
- temperature_c
- heart_rate_bpm
For the prototype, records are filtered to rows where consent_for_research is explicitly Yes. This is a coding workflow choice; because the dataset is synthetic, it is not evidence of real patient consent. Confirm the dataset's terms before use.
Requirements
Python 3.10+ is a reasonable starting point, but compatible Python and Qiskit versions can vary. Install the libraries in the same environment used to run the script:
python -m pip install qiskit qiskit-machine-learning scikit-learn pandas numpy
Run the Qiskit Classifier
1. Put qiskit_health_classifier.py and synthetic_privacy_preserving_health_dataset.csv in the same folder.
2. Open a terminal in that folder.
3. Run:
python qiskit_health_classifier.py
The script should print accuracy and a classification report for both the quantum-kernel classifier and the classical baseline, if the installed package APIs are compatible and the filtered data has enough examples per class.
Privacy and Federated Learning Notes
- Federated learning alone does not guarantee privacy.
- Differential privacy requires an appropriate mechanism, calibrated parameters, and privacy accounting.
- Secure aggregation is a separate capability and must not be claimed unless implemented and tested.
- The Qiskit starter script described here is a local classifier; it does not itself implement hospital-to-hospital communication, federated aggregation, differential privacy, or secure aggregation.
Limitations
- The dataset is synthetic and the model is experimental.
- A small dataset may produce unstable metrics or insufficient examples for some classes after filtering.
- Quantum-kernel computation can become expensive as the number of samples grows.
- No quantum advantage is claimed.
- Do not use predictions for real patient diagnosis or treatment.
Team
Epic Engineers
- Jovial Korivi — Team Leader
- Jhansi Potipadu
- Lakshmi Manaswi Jampani
- Jeswanth Aradhyula
References
- IBM Quantum Documentation: https://docs.quantum.ibm.com/
- Qiskit Machine Learning Documentation: https://qiskit-community.github.io/qiskit-machine-learning/
- Qiskit Machine Learning Quantum Kernel Tutorial: https://qiskit-community.github.io/qiskit-machine-learning/tutorials/03_quantum_kernel.html
- Scikit-learn Support Vector Machines: https://scikit-learn.org/stable/modules/svm.html
- McMahan, B. et al. (2017). Communication-Efficient Learning of Deep Networks from Decentralized Data. AISTATS.
- Dwork, C. and Roth, A. (2014). The Algorithmic Foundations of Differential Privacy.
Acknowledgments
We thank the organizers of Qiskit Fall Fest 2026, the Qiskit community, and the open-source contributors whose tools and documentation support this educational project. Add faculty or institutional acknowledgments only where applicable.
