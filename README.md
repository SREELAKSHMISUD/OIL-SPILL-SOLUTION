#0 OIL-SPILL-SOLUTION
Oil Spills are inevitable. However we try, nothing is hundred percent efficient and Oil Spills will occur. But what we can do is clean this spill at the right time in the most efficient manner. Oil spills are of different types and different oils get spilled at different circumstances. So, our project senses this spill/leak at the right time with the help of AI Sensors and turns on an alerts system and deploys drones simultaneously. These drones use laser fluorosensor and image sensing to identify the type of oil and the area of spread. Then underwater robots are used to suck in the oil (water included) and this oil is sent for further separation and Purification according to its Type and Characteristics. The advantage of using Laser Fluorosensor - remote sensing is that it works very efficiently during day time as well as during the Night. In conclusion, This Project helps to identify and clean an oil spill in the most efficient way.

Oil is one of the world's most important energy sources. It is transported by ships across the oceans and pipelines across the land due to its uneven distribution. As a result, several accidents have occurred while transporting oil to vessels, breaking pipelines, and drilling in the earth's crust.

Oil degrades the insulating ability of fur-bearing mammals, such as sea otters, as well as the water repellency of bird feathers, exposing these creatures to the elements. Birds and mammals will perish from hypothermia if they lack the ability to repel water and insulate themselves from cold water. 


WORKING PHASE 1:

   When an oil spill happens the sensors send alerts with the help of AI sensors.

The Sensing system works as Follows: 
Oils flow through pipelines. Sensors are added at Regular intervals throughout the Pipelines to monitor the flow of the oil. The Speed, Volume and Pressure of the oil is calculated between the sensors. If there is a leakage, a variation is observed in any of these characteristics. So, when there is a change of speed, pressure, etc in the flow from one sensor to another, we can easily detect that there is a Leakage in that particular area of the Pipe.


WORKING PHASE 2:

   Drones are sent from ships and images are captured by remote sensing LASER FLUOROSENSOR.
   They capture images and detect the type of oil that is spilled.
   This information is passed to the server.
   
   LASER FLUOROSENSOR works day and night.

Certain compounds, such as aromatic hydrocarbons, present in petroleum oils absorb ultraviolet laser light and become electronically excited. This excitation is quickly removed by the process of fluorescence emission, primarily in the visible region of the spectrum. By careful choice of the excitation laser wavelength and range-gated detection at selected emission wavelengths, petroleum oils can be detected and classified into three broad categories: light refined, crude or heavy refined.


WORKING PHASE 3:

  Water robots are released and then oil with water is extracted. Then oil is separated from water by extracting oil according to density,this oil can be reused further.
  sample of oil extraction, these robots extract oil according to density and water is released out, oil is reused.


MARKETING ANALYSIS


Clean up cost takes 2.4 billion to 9.4 billion dollars which was later calculated from previous oil spills as it is impossible to calculate the estimate during oil spill. By law, the parties responsible for the use, transportation, storage, and disposal of hazardous substances and oil are liable for costs. This liability applies to the cost of containment, cleanup, and damages resulting from a release related to their own activities.
However it seems, it is a complete loss for the manufacturer. Thus adapting our solution is the best way to minimize their loss and increase their profit in the long run.
We are aiming for an international marketing solution. So with the help of existing technology we focus on improving marine life by early prevention of damages caused due to oil spills. 


SUMMARY

Given the growing concern about marine oil spills and their consequences, we present to you a new solution based on existing technology: a software that detects oil spills and automatically grants access to drones and robots using artificial intelligence. As a result, we hope to be a new solution to a massive problem.


import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)


import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

import matplotlib.pyplot as plt
import seaborn as sns
df = pd.read_csv("/kaggle/input/oil-spill-detection/oil_spill.csv")
df.head()
df.isnull().sum()
df.info()
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
X = df.drop(columns = 'target')
y = df['target']
X_train,X_test,y_train,y_test = train_test_split(X,y,test_size =0.2, random_state =45)
X_train.shape
X_test.shape
from sklearn.ensemble import RandomForestClassifier
clf = RandomForestClassifier(n_estimators = 100,
                             random_state=45)
clf.fit(X_train,y_train)
from sklearn.metrics import accuracy_score
X_train_pred = clf.predict(X_train)
training_accuracy = accuracy_score(X_train_pred, y_train)
training_accuracy
X_test_pred = clf.predict(X_test)
test_accuracy = accuracy_score(X_test_pred, y_test)
test_accuracy
import tensorflow as tf
import keras
model = keras.Sequential([
                        keras.layers.Flatten(input_shape = (49,)),
                        keras.layers.Dense(500, activation='relu'),
                        keras.layers.Dense(100, activation = 'relu'),
                        keras.layers.Dense(2, activation = 'softmax')
])
model.compile(optimizer = 'Adam',
              loss = 'sparse_categorical_crossentropy',
             metrics = ['accuracy'])
r = model.fit(X_train,y_train, validation_split = 0.2, epochs=30)
plt.plot(r.history['accuracy'])
plt.plot(r.history['val_accuracy'])
plt.plot(r.history['loss'])
plt.plot(r.history['val_loss'])
y_pred = np.argmax(model.predict(X_test), axis=1)
y_pred
test_accuracy = accuracy_score(y_pred,y_test)
test_accuracy
from sklearn.metrics import precision_score
from sklearn.metrics import f1_score
test_precision = precision_score(y_pred,y_test)
test_f1 = f1_score(y_pred,y_test)
print(test_precision)
print(test_f1)
