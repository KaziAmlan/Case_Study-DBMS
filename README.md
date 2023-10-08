# Case_Study-DBMS
-- Create tables for the Gym Fitness Database

-- Members table
CREATE TABLE Members (
    MemID INT PRIMARY KEY,
    Name VARCHAR(255),
    Zip VARCHAR(10),
    MembershipPaidDate DATE
);

-- Membership types table
CREATE TABLE MembershipTypes (
    Mid INT PRIMARY KEY,
    MName VARCHAR(255),
    Price DECIMAL(10, 2)
);

-- Pass Categories table
CREATE TABLE PassCategories (
    PassCatID INT PRIMARY KEY,
    PCName VARCHAR(255),
    Price DECIMAL(10, 2)
);

-- One Day Passes table
CREATE TABLE OneDayPasses (
    PassID INT PRIMARY KEY,
    Date DATE,
    MemID INT,
    PassCatID INT,
    FOREIGN KEY (MemID) REFERENCES Members(MemID),
    FOREIGN KEY (PassCatID) REFERENCES PassCategories(PassCatID)
);

-- Merchandise table
CREATE TABLE Merchandise (
    MrchID INT PRIMARY KEY,
    Name VARCHAR(255),
    Price DECIMAL(10, 2)
);

-- Sale Transactions table
CREATE TABLE SaleTransactions (
    Tid INT PRIMARY KEY,
    Date DATE,
    MemID INT,
    FOREIGN KEY (MemID) REFERENCES Members(MemID)
);

-- Merchandise Sold in Sale Transactions table
CREATE TABLE MerchandiseSold (
    Tid INT,
    MrchID INT,
    Quantity INT,
    PRIMARY KEY (Tid, MrchID),
    FOREIGN KEY (Tid) REFERENCES SaleTransactions(Tid),
    FOREIGN KEY (MrchID) REFERENCES Merchandise(MrchID)
);

-- Relationship between Members and MembershipTypes
ALTER TABLE Members
ADD COLUMN MembershipTypeID INT,
ADD FOREIGN KEY (MembershipTypeID) REFERENCES MembershipTypes(Mid);

-- Relationship between Members and OneDayPasses
ALTER TABLE OneDayPasses
ADD FOREIGN KEY (MemID) REFERENCES Members(MemID);

-- Relationship between PassCategories and OneDayPasses
ALTER TABLE OneDayPasses
ADD FOREIGN KEY (PassCatID) REFERENCES PassCategories(PassCatID);

-- Relationship between SaleTransactions and MerchandiseSold
ALTER TABLE MerchandiseSold
ADD FOREIGN KEY (Tid) REFERENCES SaleTransactions(Tid);

-- Output foreign key information
SHOW CREATE TABLE Members;
SHOW CREATE TABLE MembershipTypes;
SHOW CREATE TABLE PassCategories;
SHOW CREATE TABLE OneDayPasses;
SHOW CREATE TABLE Merchandise;
SHOW CREATE TABLE SaleTransactions;
SHOW CREATE TABLE MerchandiseSold;
