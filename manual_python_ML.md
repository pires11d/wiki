# Python - Machine Learning
> Autor: Lucas Joshua Pires

## 1. Imports
~~~py
from sklearn.feature_extraction import CountVectorizer
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn import datasets
~~~

## 2. Splitting the dataset
~~~py
# train/test split:
from sklearn.model_selection import train_test_split
X_train,X_test,y_train,y_test = train_test_split(X, y, test_size=0.3, random_state=42)
~~~

## 3. Supervised Learning
- KNN
~~~py 
# creating the object
from sklearn.neighbors import KNeighborsClassifier
knn = KNeighborsClassifier(n_neighbors=6)
# train/test split:
from sklearn.model_selection import train_test_split
y = df['party'].values
X = df.drop('party', axis=1).values
X_train,X_test,y_train,y_test = train_test_split(X, y, test_size=0.3, random_state=21, stratify=y)
# training:
knn.fit(X_train, y_train)
# prediction:
y_pred = knn.predict(X_test)
# measuring model performance:
knn.score(X_test, y_test)
# measuring accuracy with the Confusion Matrix
from sklearn.metrics import confusion_matrix
from sklearn.metrics import classification_report
print(confusion_matrix(y_test,y_pred))
print(classification_report(y_test,y_pred))
~~~

- Linear Regression
~~~py
# creating the object
from sklearn.linear_model import LinearRegression
reg = LinearRegression()
# fitting the model
reg.fit(X_rooms, y)
# creating the prediction space
prediction_space = np.linspace(min(X_rooms),max(X_rooms)).reshape(-1,1)
plt.scatter(X_rooms, y)
plt.plot(prediction_space), reg.predict(prediction_space)
plt.show()
# plotting the correlation map
sns.heatmap(df.corr(), square=True)
# linear regression on all features
reg_all = linear_model.LinearRegression()
reg_all.fit(X_train, y_train)
y_pred = reg_all.predict(X_test)
reg_all.score(X_test, y_test)
~~~

- Cross-validation regression
~~~py
# creating the object
from sklearn import linear_model
reg = linear_model.LinearRegression
# CV scores
cv_results = cross_val_score(reg, X, y, cv=5)
~~~

- Ridge regression
~~~py
from sklearn.linear_model import Ridge
ridge = Ridge(alpha=0.1, normalize=True)
ridge.fit(X_train, y_train)
ridge_pred = ridge.predict(X_test)
ridge.score(X_test, y_test)
~~~

- Lasso regression (**BETTER**, as it drops less important coefficients!)
~~~py
from sklearn.linear_model import Lasso
lasso = Lasso(alpha=0.1, normalize=True)
lasso.fit(X_train, y_train)
lasso_pred = lasso.predict(X_test)
lasso.score(X_test, y_test)
# coefficients:
lasso_coef = lasso.coef_
~~~

- Logistic Regression
~~~py
from sklearn.linear_model import LogisticRegression
logreg = LogisticRegression()
logreg.fit(X_train,y_train)
logreg_pred = logreg.predict(X_test)
~~~

- ROC curve
~~~py
from sklearn.metrics import roc_curve
# compute predicted probabilities: y_pred_prob
y_pred_prob = logreg.predict_proba(X_test)[:,1]
# generate ROC curve values: fpr, tpr, thresholds
fpr, tpr, thresholds = roc_curve(y_test, y_pred_prob)
# plot ROC curve
plt.plot([0, 1], [0, 1], 'k--')
plt.plot(fpr, tpr)
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve')
plt.show()
~~~

- AUC (Area Under Curve)
~~~py
from sklearn.metrics import roc_auc_score
from sklearn.model_selection import cross_val_score
# auc score
roc_auc_score(y_test,y_pred_prob)
print(auc_score)
# cross-validation scores
cv_scores = cross_val_score(logreg, X, y, cv=5, scoring='roc_auc')
print(cv_scores)

#  Hyperparameter Tuning w/ GridSearchCV
from sklearn.model_selection import GridSearchCV
c_space = np.logspace(-5, 8, 15)
param_grid = {'C': c_space}
logreg_cv = GridSearchCV(logreg, param_grid, cv=5)
logreg_cv.fit(X,y)
# best parameters and best score
print(logreg_cv.best_params_)
print(logreg_cv.best_score_)
~~~

- Hyperparameter Tuning w/ RandomizedSearchCV
~~~py
from sklearn.tree import DecisionTreeClassifier
tree = DecisionTreeClassifier()
from sklearn.model_selection import RandomizedSearchCV
param_dist = {"max_depth": [3, None],
              "max_features": randint(1, 9),
              "min_samples_leaf": randint(1, 9),
              "criterion": ["gini", "entropy"]}
tree_cv = RandomizedSearchCV(tree, param_dist, cv=5)
tree_cv.fit(X,y)
# best parameters and best score
print(tree_cv.best_params_)
print(tree_cv.best_score_)
~~~

- Preprocessing Data
~~~py
from sklearn.preprocessing import Imputer
from sklearn.svm import SVC
from sklearn.pipeline import Pipeline
imp = Imputer(missing_values='NaN', strategy='most_frequent', axis=0)
# also: strategy='mean'
classifier = SVC()
steps = [('imputation',imp),('SVM',classifier)]
pipeline = Pipeline(steps)
#  Fit the pipeline to the train set
pipeline.fit(X_train,y_train)
y_pred = pipeline.predict(X_test)
~~~

- Scaling Data
~~~py
from sklearn.preprocessing import scale, StandardScaler
X_scaled = scale(X)
# norm_value = (value-mean)/std
# norm_value = (value-min)/(max-min)
~~~

## 4. Unsupervised Learning
- K-Means
~~~py
# basics:
from sklearn.cluster import KMeans
model = KMeans(n_clusters=3)
# training:
model.fit(samples)
# prediction:
labels = model.predict(samples)

# combined fit-predict:
labels = model.fit_predict(samples)

# centroids:
centroids = model.cluster_centers_

# Inertia - measuring cluster quality (how spread out they are, the lower the better)
# A good clustering has tight clusters (low inertia)... but not too many of them!
print(model.inertia_)

# cross tabulation with Pandas:
df = pd.DataFrame({'labels':labels, 'species': species})
ct = pd.crosstab(df['labels'],df['species'])
~~~

-  Standardization: commonly used as a pre-processing step
~~~py
# basics:
from sklearn.preprocessing import StandardScaler
from sklearn.cluster import KMeans	
scaler = StandardScaler()
kmeans = KMeans(n_clusters=3)
# pipeline:	
from sklearn.pipeline import make_pipeline
pipeline = make_pipeline(scaler, kmeans)
# training:
pipeline.fit(samples)
# prediction:	
labels = pipeline.predict(samples)
~~~

## 5. Deep Learning
- Regression
~~~py
from keras.layers import Dense
from keras.models import Sequential

predictors = np.loadtxt('file.csv',delimiter=',')
n_cols = predictors.shape[1]
model = Sequential()
model.add(Dense(100,activation='relu'),input_shape=(n_cols,))
model.add(Dense(100,activation='relu'))
model.add(Dense(1))
model.compile(optimizer='adam',loss='mean_squared_error')
~~~

- Classification
~~~py
from keras.layers import Dense
from keras.models import Sequential
from keras.utils import to_categorical

target = to_categorical(df.survived)
predictors = np.loadtxt('file.csv',delimiter=',')
n_cols = predictors.shape[1]
model = Sequential()
model.add(Dense(100,activation='relu'),input_shape=(n_cols,))
model.add(Dense(100,activation='relu'))
model.add(Dense(2,activation='softmax'))
model.compile(optimizer='sgd',loss='categorical_crossentropy')
~~~

- Saving/Loading the Model
~~~py
from keras.models import load_model

model.save('model.h5')
my_model = load_model('model.h5')
predictions = my_model.predict(data)
probability_true = predictions[:,1]
~~~

- Optimizing the Model
~~~py
# Defining the model generator function
def get_new_model(input_shape = input_shape):
	model = Sequential()
	model.add(Dense(100,activation='relu',input_shape=input_shape))
	model.add(Dense(100,activation='relu'))
	model.add(Dense(2,activation='softmax'))
	return(model)

# Importing the SGD optimizer
from keras.optimizers import SGD

# Creating list of learning rates: lr_to_test
lr_to_test = [0.000001, 0.01, 1]
# Looping over learning rates
for lr in lr_to_test:
	print('\n\nTesting model with learning rate: %f\n'%lr )
	model = get_new_model()
	my_optimizer = SGD(lr=lr)
	model.compile(optimizer=my_optimizer,loss='categorical_crossentropy')
	model.fit(predictors,target)
~~~

- Validating the Model
~~~py
# Splitting the dataset
model.compile(optimizer='adam',loss='categorical_crossentropy',metrics=['accuracy'])

# Fitting model
model.fit(predictors,target,validation_split=0.3)
~~~

- Early Stopping
~~~py
from keras.callbacks import EarlyStopping

early_stopping_monitor = EarlyStopping(patience=2)
model.fit(predictors,target,epochs=20,callbacks=[early_stopping_monitor])
~~~

## 6. Building a model with multiple target variables
~~~py
# splitting the data
data_to_train = df[NUMERIC_COLUMNS].fillna(-1000)
labels = pd.get_dummies(df[LABELS])
X_train,X_test,y_train,y_test = multilabel_train_test_split(data_to_train, labels, size=0.2, seed=123)

# training the model (with independent y columns)
from sklearn.linear_model import LogisticRegression
from sklearn.multiclass import OneVsRestClassifier

clf = OneVsRestClassifier(LogisticRegression())
clf.fit(X_train,y_train)

# predicting (with predict_proba)
holdout = pd.read_csv('HoldoutData.csv', index_col=0)
holdout = holdout[NUMERIC_COLUMNS].fillna(-1000)
pred = clf.predict_proba(holdout)
pred_df = pd.DataFrame(columns=pd.get_dummies(df[LABELS],prefix_sep='__'.columns),index=holdout.index,data=pred)
pred_df.to_csv('predictions.csv')
~~~

## 7. Natural Language Processing (NLP)
~~~py
from sklearn.feature_extraction.text import CountVectorizer

# create the token pattern: TOKENS_ALPHANUMERIC
TOKENS_ALPHANUMERIC = '[A-Za-z0-9]+(?=\\s+)'
TOKENS_BASIC = '\\S+(?=\\s+)'

# fill missing values in df.Position_Extra
df.Position_Extra.fillna('', inplace=True)

# instantiate the CountVectorizer: vec_alphanumeric
vec_alphanumeric = CountVectorizer(token_pattern=TOKENS_ALPHANUMERIC)
vec_basic = CountVectorizer(token_pattern=TOKENS_BASIC)

# fit to the data
vec_alphanumeric.fit(df.Position_Extra)
vec_basic.fit(df.Position_Type)

# print the number of tokens and first 15 tokens
msg = "There are {} tokens in Position_Extra if we split on non-alpha numeric"
print(msg.format(len(vec_alphanumeric.get_feature_names())))
print(vec_alphanumeric.get_feature_names()[:15])
~~~