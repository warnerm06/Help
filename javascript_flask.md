## app.py
    #NOTE: This is only part of the SQLAlchemy setup for demonstration purposes. 
    
    engine = create_engine("sqlite:///db/database_shrunk.sqlite?check_same_thread=False")
    
    Base = automap_base()
    Base.prepare(engine, reflect = True)

    #save tables as variables
    myTable = Base.classes.Tablename
    
    session = Session(engine)
    
    ......
    
    @app.route("/myurl")
    def histogram():
        """Hisogram page"""
        #query the database
        results =db.session.query(myTable.columnName).all()
        
        #turn list of lists in to a single list
        resultsList=list(np.ravel(results))
        
        #return a variable that we can work with in our html file
        return render_template("histograms.html", overall_rating=resultsList)

## index.html
    <body>
    //inline javascript to hold our variable from flask
    // note how we added the "| tojson" function
    // This is just to allow us to access the variable in our .js file. This will not show on the page. 
    <script type="text/javascript">
        var htmldata = {{ restultsList| tojson}};
    </script>
  
    // a dive with an id for our plotly 
    <div id="myDiv"></div>
    
    </body>
    // Don't forget to add a plotly CDN to the html
## javascript.js
    //javascript file. 
    var x= htmldata;

    var trace = {
        x: x,
        type: 'histogram',
      };
    var data = [trace];
    Plotly.newPlot('myDiv', data);


    
    
