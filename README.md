# fuel
code been done
import pandas
from sqlalchemy import create_engine

hostname="147.182.207.57"
uname="pythoneverything"
pwd="python123"
dbname="fuel"


engine = create_engine("mysql+pymysql://{user}:{pw}@host}/{db}"
                      .format(host=hostname, db=dbname, user=uname, pw=pwd))

tables = pandas.read_excel ('EAIaIQobChMIo__7u9LU9AIVfMmUCR3xIAqwEAAYAiAAEgIq7_D_BwE', sheet_name='Data 1',
                                  header = 2, index_col='Date')
tables.rename(columns = {'Weekly West Coast (PADD 5) Except California No 2 Diesel Ultra Low Sulfur (0-15 ppm) Retail prices (Dollars per Gallon)'
                        :'Diesel_Price'}, inplace=True)

connection=engine.connect()
tables.to_sql('Fuel', con = engine, if_exists = 'append')

engine.execute('CREATE TABLE Fuel_temp Like Fuel')
engine.execute('INSERT INTO Fel_temp SELECT DISTINCT (Date), Diesel_Price FROM Fuel')
engine.execute('DROP TABLE Fuel')
engine.execute('ALTER TABLE Fuel)temp RENAME TO Fuel')

connection.close()
