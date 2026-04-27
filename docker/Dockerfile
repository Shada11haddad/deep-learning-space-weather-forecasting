FROM nvidia/cuda:11.8.0-cudnn8-runtime-ubuntu22.04 

USER root
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y tzdata python3 python3-pip python3-dev git
RUN pip3 install --upgrade pip

# إضافة المكتبات الأساسية الناقصة (pandas, numpy, matplotlib)
RUN pip3 install pandas numpy matplotlib scipy seaborn statsmodels scikit-learn

# مكتبات المشروع والذكاء الاصطناعي
RUN pip3 install jupyter "notebook<7" nbdev voila bqplot ipympl ipyvolume
RUN pip3 install pymongo paramiko scp opencv-python regex pillow keras tensorflow torch nbeats-pytorch torch-optimizer fastai wandb

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
RUN ln -s /usr/local/cuda-11.8 /usr/local/nvidia

# إعدادات المستخدم والـ Jupyter
RUN useradd -ms /bin/bash user
RUN pip3 install jupyter_contrib_nbextensions && jupyter contrib nbextension install --user

WORKDIR /home/user
RUN jupyter notebook --generate-config

# تشغيل السيرفر بدون كلمة سر لتجنب مشاكل الـ Forbidden
CMD ["sh","-c","jupyter notebook --ip 0.0.0.0 --no-browser --allow-root --NotebookApp.token='' --NotebookApp.password=''"]