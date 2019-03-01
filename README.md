# ChessGame-Java
 public class arrays {

    public String name;
    private Field fieldObject = new Field('0', 0);

    public void Figures(String name) {                                
    this.name = name;
    };

    public void move(Field src, Field dst) {   // get name and the color of figures from src and dst + calls another
        String figurename = StringfigureChecker(src);  // move function to actually do it (so i can move the long switch
        boolean colordst = colorfigureChecker(dst);   // case to the bottom
        boolean colorsrc = colorfigureChecker(src);
        if (!src.checkEmpty()) {
            moveFigure(colordst, colorsrc, figurename, src, dst);
        }
        else System.out.println("Can't move nothing, son");
    }

    public boolean colorfigureChecker (Field a) {   //returns color of field a
        return a.getColor(a);
    }

    public String StringfigureChecker (Field a) {  // returns figure name of     field a
       return a.getFigure(a);
    }

    public void moveFigure(boolean colordst, boolean colorsrc, String figure, Field dst, Field src) {
        switch (figure) {
            case "Rookie":
                //if (colorsrc) - implement later to differentiate between     white and black movements (forward only)
                if ((dst.getY() - src.getY()) > 2) {
                    System.out.println("Rookie can't move more than two steps, ever.");
                } else if (dst.getX() - src.getX() > 1) {
                    System.out.println("Rookie can't move more than one step     to the side, ever.");
                } else if (dst.getX() - src.getX() == 1 && dst.getX() -     src.getX() == 1 && (colordst != colorsrc) && !fieldObject.checkEmpty(dst)) {     //fieldObject or dst.checkempty?
                    fieldObject.conquer(src, dst);
                    System.out.printf("Successfully beaten %s and moved to %c%d", StringfigureChecker(dst), dst.getX(), dst.getY());
                } else if (((dst.getX() - src.getX()) == 0) && ((dst.getY() - src.getY()) == 1)) {   //for the sake of testing, rework later for proper +1, +2 movements
                    fieldObject.conquer(src, dst);
                    System.out.printf("Successfully moved to %c%d",     dst.getX(), dst.getY());
                } else System.out.println("notpossibleblablatest"); //just to     check if basic movements work, complete latere
                break;


            default:
                System.out.println("defaultcase");
                break;
        }
    }
}
public class Field {


	    private char X;
	    private int Y;
	    private String figure;
	    private boolean color;  // true = white
	    private boolean empty;  // true = field is empty

	    public Field (char X, int Y) {
	        this.X = X;
	        this.Y = Y;
	    }
	    public String getFigure(Field a) {
	        return a.figure;
	    }

	    public boolean getColor(Field a) {
	        if (a.color) return true;
	        else return false;
	    }
	    public boolean checkEmpty(Field a) {
	        if (a.empty) return true;
	        else return false;
	    }
	    public void makeEmpty (Field a) {
	        a.figure = null;
	        a.empty = true;
	    }
	    public void conquer(Field src, Field dst) {
	        dst.figure = src.figure;
	        dst.color = src.color;
	    }
	}
