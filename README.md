♻️ EcoSort AI: TrashNet Waste Classification & Streamlit Web AppAn end-to-end Deep Learning computer vision solution that classifies waste into 6 distinct categories to assist automated recycling systems. Built using TensorFlow/Keras and deployed via an interactive Streamlit web application.📌 Project OverviewImproper waste segregation significantly hinders modern recycling efficiency. This project implements a regularized Convolutional Neural Network (CNN) trained on the TrashNet dataset. The model addresses severe baseline overfitting through Data Augmentation and Dropout, achieving stable generalization across unseen images.Key Features6-Class Categorization: Cardboard, Glass, Metal, Paper, Plastic, and Trash.Regularized Architecture: Integrated RandomFlip, RandomRotation, RandomZoom, and Dropout(0.3) layers.Interactive UI: Real-time visual feedback with per-class confidence breakdown using Streamlit.Zero-Dependency Deployment: Serves directly from Google Colab using native proxy integration.📊 Dataset DetailsThe model is trained on the standard TrashNet dataset (2,527 total images):Waste ClassImage CountDescriptionCardboard403Cardboard boxes, packaging materialsGlass501Clear, green, and brown glass bottles/jarsMetal410Aluminum food and beverage cansPaper594Sheets, newspaper, office paperPlastic482Plastic bottles, containers, bagsTrash137Non-recyclable miscellaneous waste🏗️ Model Architecture & TrainingInput (128, 128, 3)
│
├── Data Augmentation (RandomFlip, RandomRotation(0.2), RandomZoom(0.2))
├── Rescaling (1./255)
│
├── Conv2D (32 filters, 3x3, ReLU) ──> MaxPooling2D (2x2)
├── Conv2D (64 filters, 3x3, ReLU) ──> MaxPooling2D (2x2)
├── Conv2D (128 filters, 3x3, ReLU) ──> MaxPooling2D (2x2)
│
├── Flatten
├── Dense (128 units, ReLU)
├── Dropout (0.3)
└── Dense (6 units, Softmax Logits Output)
📈 Performance ImprovementsBaseline Model: Achieved ~84% training accuracy but suffered from severe overfitting (val_loss spiked to 1.89).Improved Regularized Model: Resolved overfitting using data augmentation and dropout, stabilizing val_loss down to 0.85 with a steady validation accuracy of ~67%.🚀 Quickstart & Local Setup1. Clone Repositorygit clone https://github.com/YOUR_USERNAME/TrashNet-Waste-Classification.git
cd TrashNet-Waste-Classification
2. Install Dependenciespip install tensorflow streamlit pillow numpy matplotlib
3. Launch Streamlit Web AppEnsure waste_classifier_improved.keras is in the project root directory, then run:streamlit run app.py
💻 Running Directly in Google ColabIf you want to host and test the web app directly inside Google Colab without installing anything locally:Open the notebook in Google Colab.Execute the model training and save cells to output waste_classifier_improved.keras.Run the Streamlit execution cell with Google's proxy helper:import subprocess
from google.colab import output

# Start Streamlit background server
subprocess.Popen(["streamlit", "run", "app.py", "--server.port=8501", "--server.headless=true"])

# Generate Google proxy link
colab_url = output.eval_js('google.colab.kernel.proxyPort(8501)')
print(f"🚀 Live Web App URL: {colab_url}")
📂 Project Structure├── app.py                         # Streamlit web interface script
├── waste_classifier_improved.keras # Saved trained model weights & architecture
├── TrashNet_Notebook.ipynb        # End-to-end training pipeline notebook
├── README.md                      # Project documentation
└── .streamlit/
    └── config.toml                # Streamlit server proxy configurations
📜 LicenseDistributed under the MIT License. See LICENSE for more information.
