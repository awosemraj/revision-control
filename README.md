# revision-control
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.FlowLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.Image;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;
import javax.swing.JPanel;
import java.lang.Object;
import com.mongodb.*;

import com.mongodb.MongoException;
import java.util.Arrays;

public class Blog1 extends JFrame
{   private static final long serialVersionUID = -948732780377948624L;
	JLabel l;
	JTextField txt;

	public void start()
	{
		l=new JLabel();
		l.setText("	Question :");
		txt=new JTextField(25);
		txt.setText("Post your Question");
		JButton but=new JButton();
		but.setText("Submit");
		String newline = "\n"; 
		add(l);
		add(txt);
		add(but);


	
		//final String str1;
		

		but.addActionListener(
	new ActionListener(){
			public void actionPerformed(ActionEvent e){
				final String str=txt.getText();
				
				txt.setText(str);
				
				
						  }
					}
				);
		String str1=txt.getText();
		setLayout(new FlowLayout());
		
	ImageImplement panel = new ImageImplement(new ImageIcon("Tulips.jpg").getImage()); 
	add(panel); 
	setVisible(true); 
	setSize(400,400);


		
			
	try{
		Mongo mongo=new Mongo("localhost" , 27017 );

          
         // Now connect to your databases
         DB db = mongo.getDB( "test" );
		 System.out.println("Connect to database successfully");
                 DBCollection coll = db.getCollection("mycol1");
         System.out.println("Collection created successfully");
       
	/**** Insert ****/
	// create a document to store key and value
	BasicDBObject document = new BasicDBObject();
	document.put("txt",str1 );
	document.put("last-blog-date", "1/9/2014");
	
	coll.insert(document);

      }catch(Exception e){
	     System.err.println( e.getClass().getName() + ": " + e.getMessage() );
	  }

		setDefaultCloseOperation(EXIT_ON_CLOSE);
	}
	
	public static void main(String args[])
	{
		new Blog1().start();
 
	}
}
class ImageImplement extends JPanel 
{
 

private Image img; 
public ImageImplement(Image img)
 { 
this.img = img; 
Dimension size = new Dimension(350,150);     //img.getWidth(null), img.getHeight(null)); 
setPreferredSize(size); 
setMinimumSize(size); 
setMaximumSize(size); 
setSize(size); 
setLayout(null); 
}
 public void paintComponent(Graphics g)
 {
 g.drawImage(img, 0, 0, null); 
}
 }

