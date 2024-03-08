# CODE

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

filepath = 'C:/Users/DELL/OneDrive/Desktop/Power BI/VNL2023.csv'
df = pd.read_csv(filepath)
df.head()

df.shape

df.describe()

# Data Preprocessing

df.isna().sum()

df.duplicated().sum()

position_counts = df["Position"].value_counts()
position_counts.index

# Plotting Pie Chart

plt.pie(position_counts,labels = position_counts.index , shadow=True,autopct = '%1.0f%%',startangle=90)
plt.title("Distribution of Position")
plt.show()

avg_attack_by_country=df.groupby("Country")["Attack"].mean()
avg_attack_by_country

block_by_country = df.groupby("Country")["Block"].mean()
#block_by_country_max = df.groupby("Country")["Block"].max()
block_by_country

avg_attack_by_country.sort_values(ascending = True).plot(kind="bar")
#avg_attack_by_country.sort_values(ascending = True).head(5).plot(kind="bar")
#avg_attack_by_country.sort_values(ascending = True).tail(5).plot(kind="bar")
plt.title("Average attack by country")
plt.xlabel("Country")
plt.ylabel("Average Attack")
plt.show()

avg_serve_by_age = df.groupby("Age")["Serve"].mean()
avg_serve_by_age.sort_values(ascending = True)

avg_serve_by_age.sort_values(ascending = False).plot(kind="bar")
#avg_serve_by_age.sort_values(ascending = False).plot(kind="pie")
plt.title("Avergae Serve by Age")
plt.ylabel("Average aserve")
plt.show()

player_name= df.groupby(["Player","Country"])["Attack"].max()
player_name

player_name.sort_values(ascending = False).head(5).plot(kind="bar")
plt.title("Maximum Attack by a Player and country")
plt.xlabel("Player and their Country")
plt.ylabel("Attack")
plt.show()

abc = df.groupby(["Player","Country","Age"])["Block"].max().head(5).plot(kind="bar")
plt.xlabel("The name and age and country of a player")
plt.ylabel("Block")
plt.show()

df.groupby(["Country","Position"])["Attack"].max().reset_index().sort_values(ascending = False , by ="Attack").head(10)

df.groupby("Country")["Dig"].sum()

# Scattered Chart

plt.scatter(df["Block"],df["Receive"])
plt.title("Block v Recieve")
plt.xlabel("Block")
plt.ylabel("Receive")
plt.show()

df.columns
#df.rename(columns={"Recieve": "-----new name---"},inplace=True)  to rename a column

# Box Plot Chart

sns.boxplot(x=df["Serve"])
plt.title("Box Plot : Distribution of serve values")
plt.xlabel("Serve")
plt.show()

# Histogram Chart

plt.hist(df["Age"],bins = 20,color="green",edgecolor="black")
plt.title("Distribution of Age")
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.show()

avg_attack_by_position = df.groupby("Position")["Attack"].mean()
avg_attack_by_position.sort_values(ascending = True).plot(kind="bar" , color = "skyblue")
plt.title("Average Attack By Position")
plt.xlabel("Position")
plt.ylabel("Attack")
plt.show()

# Line Chart

serve_trend_by_age = df.groupby("Age")["Serve"].mean()
serve_trend_by_age.plot(kind="line", marker="o", linestyle="--", color="blue" )
plt.title("Serve by Age")
plt.xlabel("Age")
plt.ylabel("Serve")
plt.show()

# Stacked Bar Chart

total_attack_block_by_country = df.groupby("Country")[["Attack","Block"]].sum()
total_attack_block_by_country.sort_values(ascending = False , by = 'Attack').plot(kind="bar",stacked =True, colormap = "viridis")
plt.title("Total Attack and Block by Country")
plt.xlabel("Country")
plt.ylabel("Total Values")
plt.show()

