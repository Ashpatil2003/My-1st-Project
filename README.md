# My-1st-Project
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# ---------------------------
# Load Dataset
# ---------------------------
df = pd.read_csv("covid_data.csv")

# Convert Date column to datetime
df["Date"] = pd.to_datetime(df["Date"])

# Sort data by date
df = df.sort_values("Date")

# ---------------------------
# Basic Analysis
# ---------------------------
total_confirmed = df["Confirmed"].max()
total_deaths = df["Deaths"].max()
total_recovered = df["Recovered"].max()

print("COVID-19 SUMMARY")
print("----------------")
print("Total Confirmed Cases:", total_confirmed)
print("Total Deaths:", total_deaths)
print("Total Recovered:", total_recovered)

# ---------------------------
# Daily New Cases Calculation
# ---------------------------
df["Daily_Confirmed"] = df["Confirmed"].diff().fillna(0)
df["Daily_Deaths"] = df["Deaths"].diff().fillna(0)
df["Daily_Recovered"] = df["Recovered"].diff().fillna(0)

# ---------------------------
# Visualization 1: Total Cases Over Time
# ---------------------------
plt.figure()
plt.plot(df["Date"], df["Confirmed"], label="Confirmed")
plt.plot(df["Date"], df["Deaths"], label="Deaths")
plt.plot(df["Date"], df["Recovered"], label="Recovered")
plt.xlabel("Date")
plt.ylabel("Cases")
plt.title("COVID-19 Total Cases Over Time")
plt.legend()
plt.show()

# ---------------------------
# Visualization 2: Daily New Confirmed Cases
# ---------------------------
plt.figure()
plt.bar(df["Date"], df["Daily_Confirmed"])
plt.xlabel("Date")
plt.ylabel("Daily New Cases")
plt.title("Daily New COVID-19 Cases")
plt.show()

# ---------------------------
# Visualization 3: Recovery Rate
# ---------------------------
df["Recovery_Rate"] = (df["Recovered"] / df["Confirmed"]) * 100

plt.figure()
plt.plot(df["Date"], df["Recovery_Rate"])
plt.xlabel("Date")
plt.ylabel("Recovery Rate (%)")
plt.title("COVID-19 Recovery Rate Over Time")
plt.show()

# ---------------------------
# Visualization 4: Death Rate
# ---------------------------
df["Death_Rate"] = (df["Deaths"] / df["Confirmed"]) * 100

plt.figure()
plt.plot(df["Date"], df["Death_Rate"])
plt.xlabel("Date")
plt.ylabel("Death Rate (%)")
plt.title("COVID-19 Death Rate Over Time")
plt.show()

# ---------------------------
# Final Insight
# ---------------------------
print("\nINSIGHTS")
print("--------")
print("Average Daily New Cases:", int(df["Daily_Confirmed"].mean()))
print("Highest Daily Spike:", int(df["Daily_Confirmed"].max()))
