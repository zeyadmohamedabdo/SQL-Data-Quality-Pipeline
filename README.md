
# 🧹 SQL Data Cleaning Project

![SQL](https://img.shields.io/badge/Language-SQL-orange?style=for-the-badge&logo=mysql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![Data](https://img.shields.io/badge/Focus-Data%20Quality-blue?style=for-the-badge)

## 📖 Project Overview
This project demonstrates how to use **SQL (Structured Query Language)** to clean and transform raw housing data into a format suitable for analysis.

The goal is to take a raw dataset containing errors, missing values, and inconsistent formatting and convert it into a standardized, usable dataset.

## 📂 The Data
The project uses the **Nashville Housing Dataset**.
* **Raw Data:** Contains issues like unusable date formats, NULL addresses, and inconsistent text fields (e.g., "Y" vs "Yes").
* **Goal:** Clean the data to prepare it for visualization in tools like Tableau or Power BI.

## ⚙️ Cleaning Steps Performed

### 1. Standardize Date Format
Converted the `SaleDate` column from a generic DateTime format to a standard Date format to remove unnecessary time data.

### 2. Populate Property Address Data
Addressed `NULL` values in the Property Address column.
* **Method:** Performed a **SELF JOIN** on the dataset to locate rows where the `ParcelID` matched but the `UniqueID` was different. If an address existed for the same ParcelID in another row, it was used to populate the missing value.

### 3. Breaking Out Address into Individual Columns
Split the `PropertyAddress` and `OwnerAddress` columns into three separate logical columns:
* **Address**
* **City**
* **State**
* **Technique:** Used `SUBSTRING` and `CHARINDEX` for property addresses, and `PARSENAME` with `REPLACE` for owner addresses.

### 4. Change "Y" and "N" to "Yes" and "No"
Standardized the `SoldAsVacant` field.
* Original data had a mix of "Yes", "Y", "No", and "N".
* Used a `CASE` statement to unify all values to "Yes" and "No".

### 5. Remove Duplicates
Identified and removed duplicate rows based on unique identifiers (ParcelID, PropertyAddress, SalePrice, SaleDate, LegalReference).
* **Technique:** Used a **CTE (Common Table Expression)** and the `ROW_NUMBER()` window function to filter out duplicates.

### 6. Delete Unused Columns
Removed columns that were no longer needed after the cleaning process (`OwnerAddress`, `TaxDistrict`, `PropertyAddress`, `SaleDate`) to streamline the dataset.

## 🧠 SQL Skills Used
* **Joins:** Self Joins to populate missing data.
* **CTEs:** For readability and handling duplicate removal logic.
* **Windows Functions:** `ROW_NUMBER`, `PARTITION BY`.
* **String Manipulation:** `PARSENAME`, `SUBSTRING`, `CHARINDEX`, `REPLACE`.
* **Data Type Conversion:** `CONVERT`, `CAST`.
* **Logic:** `CASE` Statements.

## 🚀 How to Use
1.  Download the raw data (Nashville Housing Data).
2.  Import the data into your SQL Server database.
3.  Open `Portfolio Project - Data Cleaning.sql` in SSMS (SQL Server Management Studio).
4.  Execute the queries step-by-step to clean the data.




This file is likely written for **Microsoft SQL Server (T-SQL)** because it typically uses functions like `PARSENAME` (which is unique to T-SQL) and `ISNULL`.

  * If you want to be extra precise, you can change the orange badge in the README from `SQL` to `T--SQL`.
