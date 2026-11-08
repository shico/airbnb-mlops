# Airbnb MLOps
Курсовой проект ML/DLOps.  
Данные: Inside Airbnb.  
Задача семинара: чтение CSV из S3.  

## pip команды  

pip install boto3, pandas, secretkeys  

## источник  

S3_BUCKET = "mlops26-course-bucket"  
S3_KEY = "prepared/train.csv"  
LOCAL_PATH = Path("data/train.csv")  

s3 = boto3.client(  
    "s3",  
    endpoint_url="https://storage.yandexcloud.net",  
    aws_access_key_id=KEY_ID,  
    aws_secret_access_key=ACCESS_KEY,  
    region_name="ru-central1",  
)  

## среда  

VS code, расширение Jupyter
