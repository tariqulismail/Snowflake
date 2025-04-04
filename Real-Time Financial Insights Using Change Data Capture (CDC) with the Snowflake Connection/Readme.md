{\rtf1\ansi\ansicpg1252\cocoartf2821
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fnil\fcharset0 .SFNS-Bold;\f1\fnil\fcharset0 .SFNS-Regular;\f2\fnil\fcharset0 HelveticaNeue-Bold;
\f3\froman\fcharset0 TimesNewRomanPSMT;\f4\fswiss\fcharset0 Helvetica;\f5\fmodern\fcharset0 Courier;
\f6\fnil\fcharset0 .AppleSystemUIFontMonospaced-Regular;}
{\colortbl;\red255\green255\blue255;\red14\green14\blue14;\red155\green162\blue177;\red197\green136\blue83;
\red136\green185\blue102;}
{\*\expandedcolortbl;;\cssrgb\c6700\c6700\c6700;\cssrgb\c67059\c69804\c74902;\cssrgb\c81961\c60392\c40000;
\cssrgb\c59608\c76471\c47451;}
\paperw11900\paperh16840\margl1440\margr1440\vieww28300\viewh16660\viewkind0
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs44 \cf2 AWS Kinesis Data Streams - Real-time Financial Transactions
\f1\b0\fs28 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 Overview
\f1\b0\fs28 \
\
This project demonstrates real-time data ingestion using 
\f2\b AWS Kinesis Data Streams
\f1\b0 . It includes a 
\f2\b producer
\f1\b0  to send financial transactions and a 
\f2\b consumer
\f1\b0  to process the transactions from Kinesis using Python (Boto3). The project is designed to simulate real-world financial transaction processing with anomaly detection capabilities.\
\

\f0\b\fs34 Features
\f1\b0\fs28 \
\pard\tqr\tx100\tx260\li260\fi-260\sl324\slmult1\sb240\partightenfactor0
\cf2 	\'95	
\f2\b Real-time Data Ingestion
\f1\b0  using AWS Kinesis Data Streams\
	\'95	
\f2\b Producer
\f1\b0  generates financial transaction data\
	\'95	
\f2\b Consumer
\f1\b0  reads and processes transaction data from Kinesis\
	\'95	
\f2\b Uses Trim Horizon starting position
\f1\b0  to fetch all available data from the beginning\
	\'95	
\f2\b Extensible
\f1\b0  for further analytics, anomaly detection, and visualization\
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 Architecture
\f1\b0\fs28 \
\pard\tqr\tx260\tx420\li420\fi-420\sl324\slmult1\sb240\partightenfactor0

\f3 \cf2 	1.	
\f2\b Producer:
\f1\b0  Generates synthetic financial transactions and sends them to Kinesis Data Stream.\

\f3 	2.	
\f2\b Kinesis Data Stream:
\f1\b0  Stores and streams transaction data in real-time.\

\f3 	3.	
\f2\b Consumer:
\f1\b0  Reads transactions from Kinesis, processes them, and prints/logs the output.\
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 Installation & Setup
\f1\b0\fs28 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs30 \cf2 Prerequisites
\f1\b0\fs28 \
\pard\tqr\tx100\tx260\li260\fi-260\sl324\slmult1\sb240\partightenfactor0
\cf2 	\'95	Python 3.x\
	\'95	AWS CLI configured with necessary permissions\
	\'95	Boto3 (AWS SDK for Python)\
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs30 \cf2 Install Dependencies
\f4\b0\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f5\fs28 \cf3 pip install boto3
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 Running the Project
\f1\b0\fs28 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs30 \cf2 Step 1: Create a Kinesis Data Stream
\f1\b0\fs28 \
\
Run the following AWS CLI command to create a Kinesis Data Stream:
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f5\fs28 \cf3 aws kinesis create-stream --stream-name financial-transactions-stream --shard-count 1
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs30 \cf2 Step 2: Run the Producer
\f4\b0\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f5\fs28 \cf3 python producer.py
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f1\fs28 \cf2 This script generates transaction data and sends it to Kinesis.\
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs30 \cf2 Step 3: Run the Consumer
\f4\b0\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f5\fs28 \cf3 python consumer.py
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f1\fs28 \cf2 This script reads data from Kinesis and processes it.\
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 Configuration
\f1\b0\fs28 \
\
Ensure your AWS credentials are configured properly in 
\f6 ~/.aws/credentials
\f1  or use environment variables:
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f5\fs28 \cf3 export AWS_ACCESS_KEY_ID=your-access-key\
export AWS_SECRET_ACCESS_KEY=your-secret-key\
export AWS_REGION=us-east-1
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 File Structure
\f4\b0\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f5\fs28 \cf3 \uc0\u55357 \u56514  Kinesis_Data_Streams\
 \uc0\u9500 \u9472 \u9472  producer.py  # Sends transactions to Kinesis\
 \uc0\u9500 \u9472 \u9472  consumer.py  # Reads transactions from Kinesis\
 \uc0\u9500 \u9472 \u9472  README.md    # Project documentation
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 AWS IAM Permissions Required
\f1\b0\fs28 \
\
Ensure the IAM role or user has the following permissions:
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f5\fs28 \cf3 \{\
  \cf4 "Effect"\cf3 : \cf5 "Allow"\cf3 ,\
  \cf4 "Action"\cf3 : [\
    \cf5 "kinesis:PutRecord"\cf3 ,\
    \cf5 "kinesis:PutRecords"\cf3 ,\
    \cf5 "kinesis:GetRecords"\cf3 ,\
    \cf5 "kinesis:GetShardIterator"\cf3 ,\
    \cf5 "kinesis:DescribeStream"\cf3 \
  ],\
  \cf4 "Resource"\cf3 : \cf5 "arn:aws:kinesis:us-east-1:YOUR_ACCOUNT_ID:stream/financial-transactions-stream"\cf3 \
\}
\f4\fs24 \cf0 \
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 Future Enhancements
\f1\b0\fs28 \
\pard\tqr\tx100\tx260\li260\fi-260\sl324\slmult1\sb240\partightenfactor0
\cf2 	\'95	Implement 
\f2\b Apache Flink
\f1\b0  for real-time processing and anomaly detection.\
	\'95	Store processed data in 
\f2\b AWS S3
\f1\b0  or 
\f2\b DynamoDB
\f1\b0  for further analysis.\
	\'95	Visualize transaction insights using 
\f2\b Amazon QuickSight
\f1\b0  or 
\f2\b Power BI
\f1\b0 .\
\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f0\b\fs34 \cf2 License
\f1\b0\fs28 \
\
This project is licensed under the MIT License.\
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\pardirnatural\partightenfactor0

\f4\fs24 \cf0 \
\uc0\u11835 \
\pard\tx560\tx1120\tx1680\tx2240\tx2800\tx3360\tx3920\tx4480\tx5040\tx5600\tx6160\tx6720\sl324\slmult1\pardirnatural\partightenfactor0

\f1\fs28 \cf2 \
Feel free to contribute or raise issues!\
\
\uc0\u55357 \u56960  Happy Coding! \u55356 \u57263 }