# README
---

### Purpose
This simple page is meant to be a utility for PeopleSoft developers to use to quickly generate effective date/sequence checks. Depending on the record in question, these checks can get pretty long and tedious to type out, especially when you just need some information quickly.

### Usage
Choose your database type, then what type of capitalization you want, and then input the record, its alias, and the key fields. The script will generate an effective date/sequence check based on those parameters, and you can discard the sequence portion if it's not required.

### Example
Database: Oracle
Character Case: Lower
Inputs:

	stdnt_fa_term a
	emplid
	institution
	strm

Outputs:

	and a.effdt = (
		select max(a1.effdt)
		from ps_stdnt_fa_term a1
		where 1=1
		and a1.emplid = a.emplid
		and a1.institution = a.institution
		and a1.strm = a.strm
		and a1.effdt <= sysdate)
	and a.effseq = (
		select max(a1.effseq)
		from ps_stdnt_fa_term a1
		where 1=1
		and a1.emplid = a.emplid
		and a1.institution = a.institution
		and a1.strm = a.strm
		and a1.effdt = a.effdt)

**Note:** The "where 1=1" is there only for easy of commenting out criteria. It can (and probably should) be removed from production code, for ease of future reading.