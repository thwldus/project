import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.*;

class myPanel extends JPanel implements ActionListener{
	JButton btn[][];
	JButton restart;
	JButton result;
	
	JButton addTime1;
	JButton addTime2;

	final int SIZE = 20;
	int omok[][] = new int[SIZE][SIZE];
	int turn = 0;
	int win = 0;

	int timeplus = 0;
	int addlimit1 = 1;
	int addlimit2 = 1;
	final int startTime = 10;

	private JLabel add1 = new JLabel(); //시간 추가 횟수 제한
	private JLabel add2 = new JLabel();
	private JLabel label_0 = new JLabel(); //제한시간
        private JLabel label_1 = new JLabel(); //환영문구
	private JLabel label_2 = new JLabel(); //addtime


	private JLabel order = new JLabel();
	private int on = 1; //진행중이면 1, 승패결정 시 0 
    private JProgressBar time1 = new JProgressBar(JProgressBar.HORIZONTAL, 0,10);
	private JProgressBar time2 = new JProgressBar(JProgressBar.HORIZONTAL, 0,10);

	public myPanel() {
		setLayout(null);
		setBackground(Color.LIGHT_GRAY);
		set();
	}
	public void set() {
		btn = new JButton[SIZE][SIZE];
		restart = new JButton();
		result = new JButton();
		addTime1 = new JButton();
		addTime2 = new JButton();

		for(int i=0; i<SIZE; i++) {
			for(int j=0; j<SIZE; j++) {
				btn[i][j] = new JButton();
				btn[i][j].setBounds(100+17*(j+1), 100+17*(i+1), 17, 17);
				btn[i][j].setBackground(getBackground());
				btn[i][j].addActionListener(this);
				add(btn[i][j]);				
			}
		}		
		restart.setBounds(100+17*8, 100+17*22, 100, 50);
		restart.addActionListener(this);
		restart.setText("다시 시작");
		restart.setBackground(Color.YELLOW);
		add(restart);

		addTime1.setBounds(15, 330, 90, 45);
		addTime1.addActionListener(this);
		addTime1.setText("시간 추가");
		addTime1.setBackground(Color.GRAY);
		add(addTime1);
		
		addTime2.setBounds(470, 330, 90, 45);
		addTime2.addActionListener(this);
		addTime2.setText("시간 추가");
		addTime2.setBackground(Color.GRAY);
		add(addTime2);
		
		result.setBounds(100+17*8, 100+17*9, 100, 50);
		result.setBackground(Color.GREEN);

		label_0.setBounds(220, 25, 1000, 80);
		label_1.setBounds(180, 5, 1000, 80);
		label_2.setBounds(200, 43, 1000, 80);
		add(label_0);
		add(label_1);
		add(label_2);

		order.setBounds(190, 60, 1000, 80);
		add(order);

		add1.setBounds(20,365, 90, 45);
		add(add1);
		
		add2.setBounds(470, 365, 90, 45);
		add(add2);
	
                JLabel p1 = new JLabel("◈Player 1◈");
		p1.setBounds(25, 280, 80, 20);
		add(p1);
		time1.setForeground(Color.PINK);
		time1.setBackground(getBackground());
		time1.setBounds(20, 300, 80, 20);
		time1.setValue(startTime + timeplus);
		add(time1);
		JLabel p2 = new JLabel("◈Player 2◈");
		p2.setBounds(480, 280, 80, 20);
		add(p2);
		time2.setForeground(Color.PINK);
		time2.setBackground(getBackground());
		time2.setBounds(475, 300, 80, 20);
		time2.setValue(startTime + timeplus);
		add(time2);
	}
	
	public void update() {
		int player;
		if(win==0) {
			label_0.setText("제한시간은 10초입니다.");
			label_1.setText("환영합니다! 즐거운 오목 게임 되십시오!");
			if(turn%2==0) {
				player = 1;
				order.setText("이번 차례는 플레이어" + player + " 차례입니다.");
			}
			else {
				player = 2;
				order.setText("이번 차례는 플레이어" + player + " 차례입니다.");
			}
		}
		else {
			label_0.setText(" ");
			label_1.setText("플레이어"+win+"이(가) 이겼습니다! 축하합니다!!");
			order.setText(" ");
			label_2.setText(" ");
		}
	}

	public void Win() {
		int check =0;		
		for(int i=2; i<SIZE-2; i++) {
			for(int j=2; j<SIZE-2; j++) {
					if(omok[i][j] ==1 && omok[i][j-1] == 1 && omok[i][j-2] ==1 && omok[i][j+1]==1 && omok[i][j+2] ==1) {
						check = 1;
					}else if(omok[i][j] ==2 && omok[i][j-1] == 2 && omok[i][j-2] ==2 && omok[i][j+1]==2 && omok[i][j+2] ==2) {
						check =2;
					}
					if(omok[i][j] ==1 && omok[i-1][j] == 1 && omok[i-2][j] ==1 && omok[i+1][j]==1 && omok[i+2][j] ==1) {
						check =1;
					}else if(omok[i][j] ==2 && omok[i-1][j] == 2 && omok[i-2][j] ==2 && omok[i+1][j]==2 && omok[i+2][j] ==2) {						check = 2;
				}
          		}
		}
		 
		for(int i=2; i<SIZE-2; i++) {
			for(int j=2; j<SIZE-2; j++) {
				if(omok[i][j] ==1 && omok[i-1][j-1] == 1 && omok[i-2][j-2] ==1 && omok[i+1][j+1]==1 && omok[i+2][j+2] ==1) {
					check = 1;
				}else if(omok[i][j] ==2 && omok[i-1][j-1] == 2 && omok[i-2][j-2] ==2 && omok[i+1][j+1]==2 && omok[i+2][j+2] ==2) {
					check = 2;
				}
			}
		}
		
		for(int i=2; i<SIZE-2; i++) {
			for(int j=2; j<SIZE-2; j++) {
				if(omok[i][j] ==1 && omok[i-1][j+1] == 1 && omok[i-2][j+2] ==1 && omok[i+1][j-1]==1 && omok[i+2][j-2] ==1) {
					check =1;
				}else if(omok[i][j] ==2 && omok[i-1][j+1] == 2 && omok[i-2][j+2] ==2 && omok[i+1][j-1]==2 && omok[i+2][j-2] ==2) {
					check =2;
				}
			}
		}
		
		if(check ==1) {
			win =1;
			on = 0;
		}else if(check ==2) {
			win =2;
			on = 0;
		}
		System.out.println("win: " + win);
		System.out.println("on: " + on);
		System.out.println();
		
	}
	
	public void actionPerformed(ActionEvent e) {
		for(int i=0; i<SIZE; i++) {
			for(int j=0; j<SIZE; j++) {
				if(turn %2 ==0) {
					if(omok[i][j] ==0) {
						if(e.getSource() == btn[i][j]) {
							btn[i][j].setBackground(Color.BLACK);
							omok[i][j] = 1;
							turn +=1;
						}
					}
				}else if(turn %2 ==1) {
					if(omok[i][j] ==0) {
						if(e.getSource() == btn[i][j]) {
							btn[i][j].setBackground(Color.WHITE);
							omok[i][j] = 2;
							turn +=1;
						}
					}
				}
			}
		}
		for(int i =0; i<SIZE; i++) {
			for(int j=0; j<SIZE; j++) {
				System.out.print(omok[i][j] +" ");
			}
			System.out.println();
		}
		
		if(e.getSource() == restart) {
			for(int i=0; i<SIZE; i++) {
				for(int j= 0; j<SIZE; j++) {
					btn[i][j].setBackground(getBackground());
				}
			}
			omok = new int[SIZE][SIZE];
			turn = 0;
			win = 0;
			on = 1;
			addlimit1 = 1;
			addlimit2 = 1;
			add1.setText(" ");
			add2.setText(" ");		
		}
		
		if ((addlimit1==1)&&(e.getSource() == addTime1)) {
			timeplus += 10;
			addlimit1 -= 1;
			add1.setText("시간 추가 불가");
		}
		else if ((addlimit2==1)&&(e.getSource() == addTime2)) {
			timeplus += 10;
			addlimit2 -= 1;
			add2.setText("시간 추가 불가");
		}
		

		Win();
		if(win ==1) {
			add(result);
			result.setText("P1 승리!");
		}else if(win ==2) {
			add(result);
			result.setText("P2 승리!");
		}
	}

	public void timelimit() {
		int count = 0;
		if (turn % 2 == 0) {
		    time2.setValue(startTime + timeplus);
		    timeplus = 0;
			for (int i = startTime + timeplus; i >= 1; i--) 	
				if (turn % 2 == 0) {
					try {
						Thread.sleep(1000);
					}
					catch (InterruptedException e) {	}
					count++;
					label_0.setText("제한시간 "+(startTime + timeplus-count)+"초 남았습니다.");
			        time1.setValue((startTime + timeplus-count));
				}
			if (count == startTime + timeplus) {
				add(result);
				result.setVisible(true);
				result.setText("시간초과 P2 승리");
				try {
					Thread.sleep(2000);
				}
				catch (InterruptedException e) {}
				result.setVisible(false);
				win = 2;
				on = 0;
				time1.setValue(startTime + timeplus);
			}
		}
		else if (turn % 2 == 1) {
			time1.setValue(startTime + timeplus);
			timeplus = 0;
			for (int i = startTime + timeplus; i >= 1; i--)
				if (turn % 2 == 1) {
					try {
						Thread.sleep(1000);
					}
					catch (InterruptedException e) {	}
					count++;
					label_0.setText("제한시간 "+(startTime + timeplus-count)+"초 남았습니다.");
			        time2.setValue((startTime + timeplus-count));
				}
			if (count == startTime + timeplus) {
				add(result);
				result.setVisible(true);
				result.setText("시간초과 P1 승리");
				try {
					Thread.sleep(2000);
				}
				catch (InterruptedException e) {}
				result.setVisible(false);
				win = 1;
				on = 0;
				time2.setValue(startTime + timeplus);
			}
		}	
	}
	
    public int on() { return on; }

}

public class gui {
	public static void main(String[] args) {
		JFrame frame = new JFrame();
		myPanel mp = new myPanel();
		frame.setBounds(100, 100, 600, 600);
		frame.setTitle("오목");
		frame.setVisible(true);
		frame.setDefaultCloseOperation(frame.EXIT_ON_CLOSE);
		frame.add(mp);
		while(true) {
			while(mp.on()==1){
		        mp.update();
			    mp.timelimit();
			}
			mp.update();
		}	

	}
}
