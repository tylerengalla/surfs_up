# Surfs Up 
W. Avy wants information about temperature trends before opening a surf shop. Specifically, he wants temperature data for the months of June and December in Oahu, in order to determine if the surf and ice cream shop business is sustainable year-round.

# Overview of Tech
SQLLite, SQLAlchemy, Jupyter Notebook, Pandas 

# Results

**------------June Summary ---------------------------December Summary------------**  

 ![](/june.png) ![](/december.png)

---
 
- The lowest temperature from December was only 8 degrees lower than the lowest temperature in June. There will be some cold days in both months. 
- The average tempearture for each month are relatively close to one another - only 4 degrees hotter of a difference for June. 
- The hottest temperature of both months were similar, meaning surfers will get almost as hot of days in December as June. 
- At least 50% of both months have recorded temperatures over 71 degrees in temperature 

Question is how many "pretty cold" days will slow business and how many "hot" days will make our ice cream a must have? 

# Additional Queries 
We'll categorize below 70 degree days as "pretty cold/ bad business days" and above 75 degrees as "hot/ good business days."

# June 

```python
# historically "pretty cold" days in June 
len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 6).\
filter(Measurement.tobs <= 70).all())

# Estimated cold days for June 
((len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 6).\
filter(Measurement.tobs <= 70).all()))/len(june))*31

# "hot" days in June 
len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 6).\
filter(Measurement.tobs >= 75).all())

# Estimated hot days for June 
((len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 6).\
filter(Measurement.tobs >= 75).all()))/len(june))*31
```

# December 

```python
# historically "pretty cold" days in December 
len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 12).\
filter(Measurement.tobs <= 70).all())

# Estimated cold days for December 
((len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 12).\
filter(Measurement.tobs <= 70).all()))/len(december))*31

# historically "hot" days in December 
len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 12).\
filter(Measurement.tobs >= 75).all())

# Estimated hot days for December 
((len(session.query(Measurement.date, Measurement.tobs).filter(extract("month",Measurement.date)== 12).\
filter(Measurement.tobs >= 75).all()))/len(december))*31
```
  
# Summary 

Historically speaking - the ice cream shop should be sustainable year around. Based off the 7 years of data we can estimate how many days of "good business" vs "bad business" weather days we will encounter in both June and December. June should average around 17.6 "hot" days with 3.1 "pretty cold" days. December will give us around 5.3 "hot" days with 12.9 "pretty cold" ones. 

