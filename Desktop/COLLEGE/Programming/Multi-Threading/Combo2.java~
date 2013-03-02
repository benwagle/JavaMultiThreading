import javax.swing.*;//needed for JFrame and JPanel
import java.awt.*;//needed to draw things
import java.util.*;//needed for scanner
import java.io.*;//needed for File

public class Combo2 extends JFrame
/*
 * using the swing class
 * read and print a world in game of life
 */
{
  public Combo2()
  {
    setSize(400,400);//sets the size of the window
    int h= getHeight();
    int w= getWidth();
    final boolean clock= true;
    final String same= "life6.dat";
    final String empty= "life6.dat";
    JPanel panel= new JPanel();//drawings are done on panels
    panel.setLayout(new GridLayout(2,2));
    Life life1= new Life();
    Life life2= new Life();
    Test test1= new Test();
    Test test2= new Test();
    life1.setBackground(Color.pink);
    test1.setBackground(Color.yellow);
    life2.setBackground(Color.orange);
    test2.setBackground(Color.white);
    panel.add(life1);
    panel.add(test1);
    panel.add(test2);
    panel.add(life2);
    setLocationRelativeTo(null);//GUI screen is not obscured
    setContentPane(panel);//GUIs are placed on contentPane
    setVisible(true);//enables us to view window
    Temp one = new Temp(life1, same, 2000);
    Temp1 two = new Temp1(test1, h, w, 9, clock);
    Temp three = new Temp(life2, empty,1500);
    Temp1 four= new Temp1(test2, h, w, 3, !clock);
    one.start();
    two.start();
    three.start();
    four.start();
    
  }
  
  public static void main(String[] asd)
  {
    new Combo2();
    
  }
}

class Temp extends Thread
{
  Life anim;
  String world;
  int t;
  
  public Temp(Life anim, String world, int t)
  {
    this.anim=anim;
    this.world=world;
    this.t= t;
  }
  
  public void run()
  {
    anim.begin(world,t);
  }
}

class Temp1 extends Thread
{
  Test anim1;
  int h,w,t;
  boolean clock;
  
  public Temp1(Test anim, int h,int w, int t, boolean clock)
  {
    this.anim1=anim; 
    this.h= h;
    this.w=w;
    this.t=t;
    this.clock=clock;
  }
  
  public void run()
  {
    anim1.move(h,w,t,clock);
    
  }
}

class Life extends JPanel
{
  
  final static int NROW=25, NCOL=47;
  final static char DOT= '.';
  char[][] grid= new char[NROW+2][NCOL+2];
  char[][] birth= new char[NROW+2][NCOL+2];
  boolean SameFlag = false;
  boolean BlankFlag = false;
  
  public void init()
  {
    for(int row=0; row<=NROW+1; row++)
    {
      for(int col=0; col<=NCOL+1; col++)
      {
        birth[row][col]=DOT;
      }
    }
  }
  
  public int neighbors(int r, int c)
    /*checks the current world for neighbors at each point
     * so that birth/death can be determined
     */
  {
    int count=0;
    for(int row=r-1; row<=r+1; row++)
    {
      for(int col=c-1; col<=c+1; col++)
      {
        if(grid[row][col]== 'X')
        {
          count++;
        }
      }
    }
      if(grid[r][c]=='X')
      {
        count= count-1;
      }
    return count;
    }
  
  public void print(Graphics g)
  {
    int x,y;
    y=20;
    for(int row=1; row<=NROW; row++)
    {
      x=20;
      for(int col=1; col<=NCOL; col++)
      {
        Font f = new Font("Impact", Font.ITALIC, 18);
        g.setFont(f);
        g.drawString(""+ birth[row][col],x,y);
        x= x+14;
      }
      y= y+15;
    }
  }
  
  public void pause(int t)
  {
    try
    {
      Thread.sleep(t);
    }catch(Exception ex){}
  }

  
    public void read(String world)
 {
     Scanner kbd= null;
    try
    {
        kbd= new Scanner(new File(world));
    }catch(Exception ex) {};
    
    for(int row=1; row<=NROW; row++)
    {
      String s= kbd.next();
      for(int col=1; col<=NCOL; col++)
      {
        birth[row][col]= s.charAt(col-1);
      }
    }
  }
 
 
  
  public void swap()
     {
      for(int row=1; row<=NROW; row++)
    {
      for(int col=1; col<=NCOL; col++)
       {
        grid[row][col]=birth[row][col];
        //overwrites old world with new world
       }
     }
  }
 
  
  public boolean isSame()
  {
    for(int row=1; row<=NROW; row++)
    {
      for(int col=1; col<=NCOL; col++)
      {
        if(grid[row][col]!=birth[row][col])
        {
          return false;
        }
      }
    }
    return true;
  }
  
  public boolean isEmpty()
  {
    for(int row=1; row<=NROW; row++)
    {
      for(int col=1; col<=NCOL; col++)
      {
        if(birth[row][col]=='X')
        {
          return false;
        }
      }
    }
    return true;
  }
  
  public void life()
  {
    for(int row=1; row<=NROW; row++)
    {
      for(int col=1; col<=NCOL; col++)
      {
      if(grid[row][col]=='X')
       {
         if(neighbors(row,col)==2 || neighbors(row,col)==3)
           //checks if x should be reborn
         {
           birth[row][col]='X';
         }
         if(neighbors(row,col)!=2 && neighbors(row,col)!=3)
           //checks if x should die
         {
           birth[row][col]=DOT;
         }
       }
       if(grid[row][col]==DOT)
       {
         if(neighbors(row,col)==3)
           //checks if x should be born
         {
           birth[row][col]='X';
         }
         if(neighbors(row,col)!=3)
           //checks if dot stays dead
         {
           birth[row][col]=DOT;
         }
       }
      }
    }
  }
  
  public void begin(String world, int t) 
  {
    init();
    repaint();
    pause(t);
    read(world);
    repaint();
    do
    {
    swap();
    pause(t);
    life();
    repaint();
    }while(!isSame() && !isEmpty());
     
    if(isSame())
    {
      SameFlag = true;
      repaint();
    }
    
    if(isEmpty())
    {
      BlankFlag = true;
      repaint();
    }
  }
  

  public void paintComponent(Graphics g)//initially called by JVM
  {
    super.paintComponent(g);//erases previous window
    g.setColor(Color.black);
    print(g);
    if(SameFlag)
        {
          Font f = new Font("Impact", Font.ITALIC, 36);
          g.setFont(f);
          g.drawString("The worlds are repeating!",10,450);
        }
       if(BlankFlag)
        {
          g.drawString("The world is blank!",10,450);
        }
  }

}

class Test extends JPanel
{
  int x=0;
  int y=200;
  
  public void move(int h, int w, int t, boolean clock)
  {
    while(clock)
    {
      if(x==0)
      {
        while(y<h)
        {
          x++;
          y++;
          repaint();//calls paintComponent
          try
          {
            Thread.sleep(t);//100 milliseconds
          }catch(Exception ex){};
        }
      }
        
       
      
      if(y==h)
        {
          while(y>0 && x<w)
          {
            x++;
            y--;
            repaint();
            try
            {
              Thread.sleep(t);//100 milliseconds
            }catch(Exception ex){};
          }
        }
      
      
      
      if(x==w)
      {
        while(y>0 && x>0)
        {
          x--;
          y--;
          repaint();
          try
          {
            Thread.sleep(t);//100 milliseconds
          }catch(Exception ex){};
        }
      }
      
      
      if(y==0)
      {
        while(y<h && x>0)
        {
          x--;
          y++;
          repaint();//calls paintComponent
          try
          {
            Thread.sleep(t);//100 milliseconds
          }catch(Exception ex){};
        }
      }
    
    }
    while(!clock)
    {
      
      
      if(x==0)
      {
        while(y>0)
        {
          x++;
          y--;
          repaint();//calls paintComponent
          try
          {
            Thread.sleep(t);//100 milliseconds
          }catch(Exception ex){};
        }
      }
        
       
      
      if(y==h)
        {
          while(y>0 && x>0)
          {
            x--;
            y--;
            repaint();
            try
            {
              Thread.sleep(t);//100 milliseconds
            }catch(Exception ex){};
          }
        }
      
      
      
      if(x==w)
      {
        while(y<h && x>0)
        {
          x--;
          y++;
          repaint();
          try
          {
            Thread.sleep(t);//100 milliseconds
          }catch(Exception ex){};
        }
      }
      
      
      if(y==0)
      {
        while(y<h && x<w)
        {
          x++;
          y++;
          repaint();//calls paintComponent
          try
          {
            Thread.sleep(t);//100 milliseconds
          }catch(Exception ex){};
        }
      }
    
    }
  }
          
     
public void paintComponent(Graphics g)
  {
    int k= 10;
    g.setColor(Color.red);
    super.paintComponent(g);//erases previous window
    g.setColor(Color.red);
    g.fillRect(x,y,k,k);
    g.setColor(Color.black);
    g.drawLine(0,409, 409, 409);
    g.drawLine(409,0,409,409);
  }
}