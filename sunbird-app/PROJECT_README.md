PS C:\Users\HP\Desktop\merged_projects\internship-assessment> python -m venv venv            
PS C:\Users\HP\Desktop\merged_projects\internship-assessment> .\venv\Scripts\Activate.ps1
(venv) PS C:\Users\HP\Desktop\merged_projects\internship-assessment> pip install -r requirements.txt

(venv) PS C:\Users\HP\Desktop\merged_projects\internship-assessment> streamlit run app.py                                     
Usage: streamlit run [OPTIONS] [TARGET] [ARGS]...
Try 'streamlit run --help' for help.

Error: Invalid value: File does not exist: app.py
(venv) PS C:\Users\HP\Desktop\merged_projects\internship-assessment> cd sunbird-app          
(venv) PS C:\Users\HP\Desktop\merged_projects\internship-assessment\sunbird-app> streamlit run app.py
2026-05-15 12:47:38.462 Uvicorn server started on 0.0.0.0:8501

  You can now view your Streamlit app in your browser.

  Local URL: http://localhost:8501
  Network URL: http://192.168.1.112:8501


  Working deployed link: https://huggingface.co/spaces/delight2004/sunbird_app

  