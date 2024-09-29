# Verify Account Positions Automation for ACME Systems Inc.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)


## Introduction

Welcome to the **Verify Account Positions Automation** project for ACME Systems Inc. This project automates the verification of account positions for clients at ACME Systems Inc. using UiPath's Robotic Enterprise Framework (REFramework). The automation process involves comparing transactions between System 1 (Web Application) and System 3 (Desktop Application), identifying discrepancies, and updating the transaction status accordingly. By leveraging Orchestrator queues, the solution ensures efficient workload distribution, robust exception handling, and seamless integration with existing systems.
**The components for ![ACME1](https://github.com/SomiaAbdelhakim/ACME1-System-Library) and ACME3 have been developed as reusable modules, which are seamlessly integrated into the overall automation workflow.**

## Features

- **Automated Transaction Verification:** Compares account transactions between System 1 (Web Application) and System 3 (Desktop Application).
- **Exception Handling:** Differentiates and handles Business Rule Exceptions and System Exceptions effectively.
- **Orchestrator Queue Integration:** Manages transactions using Orchestrator queues for scalability and reliability.
- **Comprehensive Logging:** Detailed logs for monitoring and diagnosing issues via UiPath Orchestrator.

## Architecture

The automation follows the Robotic Enterprise Framework (REFramework) structure, which includes the following key states:
- **Init:** Initializes settings, application, and retrieves initial data.
- **Get Transaction Data:** Retrieves transaction items from the Orchestrator queue.
- **Process Transaction:** Processes each transaction item, handles exceptions, and updates transaction status.
- **End Process:** Closes applications and performs cleanup tasks.

## Prerequisites

- **UiPath Studio:** Ensure you have UiPath Studio installed.
- **UiPath Orchestrator:** Access to UiPath Orchestrator for queue management and robot orchestration.
- **Access Credentials:** Necessary credentials to access System 1 and System 3 applications.
- **Configuration Files:** Access to the provided `Config.xlsx` and CSV files containing test data.


--------------------------------------------------------------------------------------------------------------------------------------
<be>

### REFrameWork Template ###
**Robotic Enterprise Framework**

* Built on top of *Transactional Business Process* template
* Uses *State Machine* layout for the phases of automation project
* Offers high level logging, exception handling and recovery
* Keeps external settings in *Config.xlsx* file and Orchestrator assets
* Pulls credentials from Orchestrator assets and *Windows Credential Manager*
* Gets transaction data from Orchestrator queue and updates back status
* Takes screenshots in case of system exceptions


### How It Works ###

1. **INITIALIZE PROCESS**
 + ./Framework/*InitiAllSettings* - Load configuration data from Config.xlsx file and from assets
 + ./Framework/*GetAppCredential* - Retrieve credentials from Orchestrator assets or local Windows Credential Manager
 + ./Framework/*InitiAllApplications* - Open and login to applications used throughout the process

2. **GET TRANSACTION DATA**
 + ./Framework/*GetTransactionData* - Fetches transactions from an Orchestrator queue defined by Config("OrchestratorQueueName") or any other configured data source

3. **PROCESS TRANSACTION**
 + *Process* - Process trasaction and invoke other workflows related to the process being automated 
 + ./Framework/*SetTransactionStatus* - Updates the status of the processed transaction (Orchestrator transactions by default): Success, Business Rule Exception or System Exception

4. **END PROCESS**
 + ./Framework/*CloseAllApplications* - Logs out and closes applications used throughout the process


### For New Project ###

1. Check the Config.xlsx file and add/customize any required fields and values
2. Implement InitiAllApplications.xaml and CloseAllApplicatoins.xaml workflows, linking them in the Config.xlsx fields
3. Implement GetTransactionData.xaml and SetTransactionStatus.xaml according to the transaction type being used (Orchestrator queues by default)
4. Implement Process.xaml workflow and invoke other workflows related to the process being automated
