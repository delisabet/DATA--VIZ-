DATA--VIZ-
==========
// This code was borrowed from the tutorial Data visualization at lymda.com and modified. http://www.lynda.com/course20/Processing-tutorials/Generating-dot-plots/97578/113208-4.html
// // Ex11_01

color[] Sonia= {#2e0927, #d90000, #ff2d00, #073a73, #04756f};
color[] palette = Sonia;
PFont labelFont;

Table stateData;
int rowCount;
int d = 50;

void setup() {
  size(800, 400);
  stateData = new Table("stateData.tsv");
  rowCount = stateData.getRowCount();
  println("rowCount = " + rowCount);
  labelFont = loadFont("Monospaced-18.vlw");
}

void draw() {
  background(palette[0]);
  textFont(labelFont);
  stroke(0,0,0);
  fill(20);
  textAlign(CENTER);

for (int i = 0; i < 8; i++) {
  line(i * 80 + 100, 20, i * 80 + 100, height - 30);
  text (i-2, i * 80 + 100, height - 10);
}

  smooth();
 

  for (int row = 0; row < rowCount; row++) {
    // State names
    String state = stateData.getString(row, 0);
    
    // NFL
    float nfl = (stateData.getFloat(row,  9) + 2) * 65 + 100;
    fill(palette[1], 160);
    ellipse(nfl, height*.2, d, d);
    text("nfl", 60, height*.2+5);
    if(dist(nfl, height*.2, mouseX, mouseY) < (d/2+1)) {
      text(state, nfl, height*.2 - 10);
    }

    // NBA
    float nba = (stateData.getFloat(row, 10) + 2) * 65 + 100;
    fill(palette[2], 160);
    ellipse(nba, height*.4, d, d);
    text("nba", 60, height*.4+5);
    if(dist(nba, height*.4, mouseX, mouseY) < (d/2+1)) {
      text(state, nba, height*.4 - 10);
    }

    // MLB
    float mlb = (stateData.getFloat(row, 11) + 2) * 65 + 100;
    fill(palette[3], 160);
    ellipse(mlb, height*.6, d, d);
    text("mlb", 60, height*.6+5);
    if(dist(mlb, height*.6, mouseX, mouseY) < (d/2+1)) {
      text(state, mlb, height*.6 - 10);
    }

    // MLS
    float mls = (stateData.getFloat(row, 12) + 2) * 65 + 100;
    fill(palette[4], 160);
    ellipse(mls, height*.8, d, d);
    text("mls", 60, height*.8+5);
    if(dist(mls, height*.8, mouseX, mouseY) < (d/2+1)) {
      text(state, mls, height*.8 - 10);
    }
  }
}



class Table {
  int rowCount;
  String[][] data;
  
  
  Table(String filename) {
    String[] rows = loadStrings(filename);
    data = new String[rows.length][];
    
    for (int i = 0; i < rows.length; i++) {
      if (trim(rows[i]).length() == 0) {
        continue; // skip empty rows
      }
      if (rows[i].startsWith("#")) {
        continue;  // skip comment lines
      }
      
      // split the row on the tabs
      String[] pieces = split(rows[i], TAB);
      // copy to the table array
      data[rowCount] = pieces;
      rowCount++;
      
      // this could be done in one fell swoop via:
      //data[rowCount++] = split(rows[i], TAB);
    }
    // resize the 'data' array as necessary
    data = (String[][]) subset(data, 0, rowCount);
  }
  
  
  int getRowCount() {
    return rowCount;
  }
