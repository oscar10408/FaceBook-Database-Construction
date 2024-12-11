# Facebook Database Project

## Overview

In **Project 1**, I designed a relational database for the fictional social media platform **Fakebook**. The project involved creating an ER diagram based on the provided business rules and implementing SQL scripts to create, load, and drop database objects.

## Key Features

- **Users**: I modeled user profiles, including personal information, educational history, and friendships.
- **Messages**: I tracked messages between users, including sender and receiver details.
- **Photos and Albums**: I handled photo uploads into albums, with user tagging and album metadata.
- **Events**: I modeled events, event participation, and related metadata such as time and location.

## Objectives

1. **ER Diagram**: I created an ER diagram representing the business rules of the Fakebook platform.
2. **SQL Scripts**: I wrote SQL scripts to create, load, and drop database objects according to the ER diagram.


## Part 1: Creating an ER Diagram

For this part, I designed an ER diagram that accurately reflects the key features of Fakebook:

1. **Users**: 
   - Each user has a profile with personal info, educational history, and a list of friends. The friends are modeled using a "Requester" and "Requestee" relationship.
2. **Messages**: 
   - Each message has a unique ID, and tracks the sender and receiver along with the message content and timestamp.
3. **Photos and Albums**: 
   - Photos are part of albums, with metadata such as timestamps, captions, and tagged users. Users can be tagged in photos at specific coordinates.
4. **Events**: 
   - Events are created by users, and I tracked participants with their confirmation status, as well as event details like location and time.

## Deliverables

- **ER Diagram**: A diagram that clearly depicts entities, attributes, relationships, and constraints.
- **SQL Scripts**: Scripts to create the database schema, load data, and manage objects.

## Notes

- I ensured that the ER diagram accurately represented the required relationships and constraints.
- While some constraints couldn’t be directly modeled in the ER diagram, I implemented them later through SQL scripts.

## Part 2: Creating the Data Tables

## Overview
For the second task of Project 1, you are required to write SQL DDL (Data Definition Language) statements to create and drop data tables that reflect the **Fakebook** specifications. You will need to write two SQL scripts:

1. **createTables.sql**: This script will create the necessary data tables.
2. **dropTables.sql**: This script will drop (destroy) the data tables.

These scripts should also create and drop any necessary constraints, sequences, and triggers required to enforce the rules defined in the Fakebook specification.

## Steps

### 1. Writing the SQL Scripts
You should create two SQL scripts:

- **createTables.sql**: This script will:
  - Create all the necessary tables.
  - Create any required constraints (such as foreign keys).
  - Create sequences and triggers needed to enforce database rules.

- **dropTables.sql**: This script will:
  - Drop all the tables created in `createTables.sql`.
  - Drop the corresponding constraints, sequences, and triggers.

### 2. Running the Scripts
Once you have written the two SQL scripts, follow the steps below to run them using SQL*Plus on your Linux machine.
   ```sql
   SQL> @createTables
   SQL> @dropTables
   ```

##  Desired Schema
# Fakebook Database Schema

## Users Table

| Column           | Type        | Required |
|------------------|-------------|----------|
| user_id          | INTEGER     | yes      |
| first_name       | VARCHAR2(100)| yes      |
| last_name        | VARCHAR2(100)| yes      |
| year_of_birth    | INTEGER     | yes      |
| month_of_birth   | INTEGER     | yes      |
| day_of_birth     | INTEGER     | yes      |
| gender           | VARCHAR2(100)| yes      |

## Friends Table

| Column     | Type    | Required |
|------------|---------|----------|
| user1_id   | INTEGER | yes      |
| user2_id   | INTEGER | yes      |

**Important**: This table should not allow duplicate friendships. The combination `(user1_id, user2_id)` and `(user2_id, user1_id)` should be treated as the same.

## Cities Table

| Column       | Type        | Required |
|--------------|-------------|----------|
| city_id      | INTEGER     | yes      |
| city_name    | VARCHAR2(100)| yes      |
| state_name   | VARCHAR2(100)| yes      |
| country_name | VARCHAR2(100)| yes      |

## User_Current_Cities Table

| Column        | Type    | Required |
|---------------|---------|----------|
| user_id       | INTEGER | yes      |
| current_city_id | INTEGER | yes    |

## User_Hometown_Cities Table

| Column           | Type    | Required |
|------------------|---------|----------|
| user_id          | INTEGER | yes      |
| hometown_city_id | INTEGER | yes      |

## Messages Table

| Column          | Type        | Required |
|-----------------|-------------|----------|
| message_id      | INTEGER     | yes      |
| sender_id       | INTEGER     | yes      |
| receiver_id     | INTEGER     | yes      |
| message_content | VARCHAR2(2000)| yes    |
| sent_time       | TIMESTAMP   | yes      |

## Programs Table

| Column         | Type        | Required |
|----------------|-------------|----------|
| program_id     | INTEGER     | yes      |
| institution    | VARCHAR2(100)| yes     |
| concentration  | VARCHAR2(100)| yes     |
| degree         | VARCHAR2(100)| yes     |

## Education Table

| Column       | Type        | Required |
|--------------|-------------|----------|
| user_id      | INTEGER     | yes      |
| program_id   | INTEGER     | yes      |
| program_year | INTEGER     | yes      |

## User_Events Table

| Column           | Type        | Required |
|------------------|-------------|----------|
| event_id         | INTEGER     | yes      |
| event_creator_id | INTEGER     | yes      |
| event_name       | VARCHAR2(100)| yes     |
| event_tagline    | VARCHAR2(100)| no      |
| event_description| VARCHAR2(100)| no      |
| event_host       | VARCHAR2(100)| no      |
| event_type       | VARCHAR2(100)| no      |
| event_subtype    | VARCHAR2(100)| no      |
| event_address    | VARCHAR2(2000)| no     |
| event_city_id    | INTEGER     | yes      |
| event_start_time | TIMESTAMP   | no      |
| event_end_time   | TIMESTAMP   | no      |

## Participants Table

| Column        | Type        | Required |
|---------------|-------------|----------|
| event_id      | INTEGER     | yes      |
| user_id       | INTEGER     | yes      |
| confirmation  | VARCHAR2(100)| yes     |

**Important**: The value of `confirmation` must be one of the following: `Attending`, `Unsure`, `Declines`, `Not_Replied`.

## Albums Table

| Column             | Type        | Required |
|--------------------|-------------|----------|
| album_id           | INTEGER     | yes      |
| album_owner_id     | INTEGER     | yes      |
| album_name         | VARCHAR2(100)| yes     |
| album_created_time | TIMESTAMP   | yes      |
| album_modified_time| TIMESTAMP   | no      |
| album_link         | VARCHAR2(2000)| yes    |
| album_visibility   | VARCHAR2(100)| yes     |
| cover_photo_id     | INTEGER     | yes      |

**Important**: The value of `album_visibility` must be one of the following: `Everyone`, `Friends`, `Friends_Of_Friends`, or `Myself`.

## Photos Table

| Column             | Type        | Required |
|--------------------|-------------|----------|
| photo_id           | INTEGER     | yes      |
| album_id           | INTEGER     | yes      |
| photo_caption      | VARCHAR2(2000)| no     |
| photo_created_time | TIMESTAMP   | yes      |
| photo_modified_time| TIMESTAMP   | no      |
| photo_link         | VARCHAR2(2000)| yes    |

## Tags Table

| Column           | Type        | Required |
|------------------|-------------|----------|
| tag_photo_id     | INTEGER     | yes      |
| tag_subject_id   | INTEGER     | yes      |
| tag_created_time | TIMESTAMP   | yes      |
| tag_x            | NUMBER      | yes      |
| tag_y            | NUMBER      | yes      |

