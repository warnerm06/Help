## index.html
    
## Database Set up
engine = create_engine("sqlite:///db/database_shrunk.sqlite?check_same_thread=False")

Base = automap_base()
Base.prepare(engine, reflect = True)

#save tables as variables
Player = Base.classes.Player
Player_Attributes = Base.classes.Player_Attributes

session = Session(engine)
    
    
