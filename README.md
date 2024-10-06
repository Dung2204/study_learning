from sklearn.feature_extraction.text import CountVectorizer #hoa vector text
from sklearn.naive_bayes import MultinomialNB
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
import joblib

df = pd.read_csv("https://raw.githubusercontent.com/amankharwal/Website-data/master/dataset.csv")

X = np.array(df["Text"])
Y = df["language"]

# print(Y.value_counts())  // dem xem co bao nhieu ngon ngu va van ban

cv = CountVectorizer()  #vector hoa text

X = cv.fit_transform(X)

X_train , X_test , Y_train , Y_test = train_test_split(X,Y, test_size=0.2, random_state=43)

model = MultinomialNB()

model.fit(X_train,Y_train)

Y_pred = model.predict(X_test)

# print(f"Accuracy: {100*accuracy_score(Y_pred,Y_test):.2f}%")      #kiem tra accuracy bao nhieu %

Users = input("Nhap van ban: ")

test = cv.transform([Users]).toarray()   # vector hoa text
# print(test)                              # in ra cac text da hoa vector dang 0 1

output = model.predict(test)
print(output)
