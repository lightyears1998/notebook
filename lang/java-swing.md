# Java Swing

```java
import java.awt.*;
import java.awt.event.*;  // 事件机制

import javax.swing.*;
```

FlowLayout “如果可能，一字排开；位置不够，自动换行”

```java
public class TestFlowLayout {
    public static void main(String[] args) {
        JFrame f = new JFrame("Frame Layout");
        JButton button1 = new JButton("确定");
        JButton button2 = new JButton("打开");
        JButton button3 = new JButton("关闭");
        JButton button4 = new JButton("取消");
        f.setLayout(new FlowLayout());

        f.add(button1);
        f.add(button2);
        f.add(button3);
        f.add(button4);

        f.setSize(100, 100);
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}

```

BorderLayout “按东南西北排列”

```java
import javax.swing.*;
import java.awt.*;

public class BorderLayoutWindow extends JFrame {
    public BorderLayoutWindow() {
        setLayout(new BorderLayout());
        add(new JButton("North"), BorderLayout.NORTH);
        add(new JButton("South"), BorderLayout.SOUTH);
        add(new JButton("West"), BorderLayout.WEST);
        add(new JButton("East"), BorderLayout.EAST);
        add(new JButton("Center"), BorderLayout.CENTER);
    }

    public static void main(String[] args) {
        BorderLayoutWindow window = new BorderLayoutWindow();
        window.setTitle("BorderLayout Application");
        window.pack();
        window.setVisible(true);
        window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```

GridLayout “构造指定行列的网格，在网格中排列组件”

```java
import javax.swing.*;
import java.awt.*;

public class GridLayoutWindow extends JFrame {
    GridLayoutWindow() {
        setLayout(new GridLayout(3, 2));  // 在3行2列的网格中排列组件
        for (int i = 1; i <= 6; ++i) {
            add(new JButton(new Integer(i).toString()));
        }
    }

    public static void main(String[] args) {
        GridLayoutWindow window = new GridLayoutWindow();
        window.setTitle("GridLayout Application");
        window.pack();
        window.setVisible(true);
        window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```

ActionListener

```java
public class TestActionEvent {
    public static void main(String[] args) {
        JFrame f = new JFrame("Test");

        JButton minusBtn = new JButton("-");
        JButton plusBtn = new JButton("+");
        JLabel counterLb = new JLabel("0", JLabel.CENTER);

        Monitor monitor = new Monitor();
        monitor.setCounterLabel(counterLb);
        minusBtn.setActionCommand("-");
        minusBtn.addActionListener(monitor);
        plusBtn.setActionCommand("+");
        plusBtn.addActionListener(monitor);

        f.setLayout(new GridLayout());
        f.add(minusBtn);
        f.add(counterLb);
        f.add(plusBtn);
        f.pack();
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}

class Monitor implements ActionListener {
    int counter = 0;
    JLabel counterLabel;

    public void setCounterLabel(JLabel label) {
        this.counterLabel = label;
    }

    private void updateCounterLabel() {
        if (counterLabel != null) {
            counterLabel.setText(new Integer(counter).toString());
        }
    }

    public void actionPerformed(ActionEvent e) {
        String command = e.getActionCommand();
        if (command.equals("-")) {
            if (counter > 0) {
                counter--;
            }
        } else if (command.equals("+")) {
            counter++;
        }
        updateCounterLabel();
    }
}
```

MenuBar, Menu and MenuItem “可以在Menu中添加Menu以实现菜单的嵌套”

```java
public class MenuTest {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Window with Menu");
        JMenuBar menuBar = new JMenuBar();
        frame.setJMenuBar(menuBar);

        JMenu menu1 = new JMenu("File");
        JMenu menu2 = new JMenu("Edit");
        JMenu menu3 = new JMenu("Help");
        menuBar.add(menu1);
        menuBar.add(menu2);
        menuBar.add(menu3);

        menu1.add(new JMenuItem("New"));
        menu1.add(new JMenuItem("Save"));
        menu1.add(new JMenuItem("Load"));
        menu1.addSeparator();
        menu1.add(new JMenuItem("Quit"));

        frame.pack();
        frame.setVisible(true);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```
