# DarkChess
package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

public class AdvisorChessComponent extends ChessComponent {

    public AdvisorChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
        if (this.getChessColor() == ChessColor.RED) {
            name = "仕";
        } else {
            name = "士";
        }
    }
}
package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

public class CannonChessComponent extends ChessComponent {
    public CannonChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
        if (this.getChessColor() == ChessColor.RED) {
            name = "炮";
        } else {
            name = "砲";
        }
    }

    @Override
    public boolean canMoveTo(SquareComponent[][] chessboard, ChessboardPoint destination) {
        SquareComponent destinationChess = chessboard[destination.getX()][destination.getY()];
        int x = this.getChessboardPoint().getX();
        int y = this.getChessboardPoint().getY();
        boolean toUp = false;
        boolean toDown = false;
        boolean toLeft = false;
        boolean toRight = false;
        if (x - destination.getX() >= 2 && y == destination.getY()) {
            int counter = 0;
            for (int i = destination.getX() + 1; i < x; i++) {
                if (!(chessboard[i][y] instanceof EmptySlotComponent)) counter++;
            }
            if (counter == 1) toUp = true;
            else toUp = false;
        }
        if (destination.getX() - x >= 2 && y == destination.getY()) {
            int counter = 0;
            for (int i = x + 1; i < destination.getX(); i++) {
                if (!(chessboard[i][y] instanceof EmptySlotComponent)) counter++;
            }
            if (counter == 1) toDown = true;
            else toDown = false;
        }
        if (y - destination.getY() >= 2 && x == destination.getX()) {
            int counter = 0;
            for (int i = destination.getY() + 1; i < y; i++) {
                if (!(chessboard[x][i] instanceof EmptySlotComponent)) counter++;
            }
            if (counter == 1) toLeft = true;
            else toLeft = false;
        }
        if (destination.getY() - y >= 2 && x == destination.getX()) {
            int counter = 0;
            for (int i = y + 1; i < destination.getY(); i++) {
                if (!(chessboard[x][i] instanceof EmptySlotComponent)) counter++;
            }
            if (counter == 1) toRight = true;
            else toRight = false;
        }
        boolean isEmpty;
        if (destinationChess instanceof EmptySlotComponent) isEmpty = true;
        else isEmpty = false;
        if ((toUp || toDown || toLeft || toRight) && !isEmpty) return true;
        else return false;
    }
}
package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

/**
 * 表示黑红车
 */
public class ChariotChessComponent extends ChessComponent {

    public ChariotChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
        if (this.getChessColor() == ChessColor.RED) {
            name = "俥";
        } else {
            name = "車";
        }
    }
}

package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

/**
 * 表示棋盘上非空棋子的格子，是所有非空棋子的父类
 */
public class ChessComponent extends SquareComponent{
    protected String name;// 棋子名字：例如 兵，卒，士等

    @Override
    public String getName() {
        return name;
    }

    protected ChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
    }
    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        //绘制棋子填充色
        g.setColor(Color.ORANGE);
        g.fillOval(spacingLength, spacingLength, this.getWidth() - 2 * spacingLength, this.getHeight() - 2 * spacingLength);
       //绘制棋子边框
        g.setColor(Color.DARK_GRAY);
        g.drawOval(spacingLength, spacingLength, getWidth() - 2 * spacingLength, getHeight() - 2 * spacingLength);

        if (isReversal) {
            //绘制棋子文字
            g.setColor(this.getChessColor().getColor());
            g.setFont(CHESS_FONT);
            g.drawString(this.name, this.getWidth() / 4, this.getHeight() * 2 / 3);

            //绘制棋子被选中时状态
            if (isSelected()) {
                g.setColor(Color.RED);
                Graphics2D g2 = (Graphics2D) g;
                g2.setStroke(new BasicStroke(4f));
                g2.drawOval(spacingLength, spacingLength, getWidth() - 2 * spacingLength, getHeight() - 2 * spacingLength);
            }
        }
    }
}

package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

/**
 * 这个类表示棋盘上的空棋子的格子
 */
public class EmptySlotComponent extends SquareComponent {

    public EmptySlotComponent(ChessboardPoint chessboardPoint, Point location, ClickController listener, int size) {
        super(chessboardPoint, location, ChessColor.NONE, listener, size);
    }

    @Override
    public boolean canMoveTo(SquareComponent[][] chessboard, ChessboardPoint destination) {
        return false;
    }

}


package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

public class GeneralChessComponent extends ChessComponent {
    public GeneralChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
        if (this.getChessColor() == ChessColor.RED) {
            name = "帥";
        } else {
            name = "将";
        }
    }
}

package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

public class HorseChessComponent extends ChessComponent {

    public HorseChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
        if (this.getChessColor() == ChessColor.RED) {
            name = "傌";
        } else {
            name = "馬";
        }
    }
}

package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

public class MinisterChessComponent extends ChessComponent {

    public MinisterChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
        if (this.getChessColor() == ChessColor.RED) {
            name = "相";
        } else {
            name = "象";
        }
    }
}

package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import java.awt.*;

public class SoldierChessComponent extends ChessComponent {
    public SoldierChessComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        super(chessboardPoint, location, chessColor, clickController, size);
        if (this.getChessColor() == ChessColor.RED) {
            name = "兵";
        } else {
            name = "卒";
        }
    }
}

package chessComponent;

import controller.ClickController;
import model.ChessColor;
import model.ChessboardPoint;

import javax.swing.*;
import java.awt.*;
import java.awt.event.MouseEvent;

/**
 * 这个类是一个抽象类，主要表示8*4棋盘上每个格子的棋子情况。
 * 有两个子类：
 * 1. EmptySlotComponent: 空棋子
 * 2. ChessComponent: 表示非空棋子
 */
public abstract class SquareComponent extends JComponent {

    private static final Color squareColor = new Color(250, 220, 190);
    protected static int spacingLength;
    protected static final Font CHESS_FONT = new Font("黑体", Font.BOLD, 36);

    /**
     * chessboardPoint: 表示8*4棋盘中，当前棋子在棋格对应的位置，如(0, 0), (1, 0)等等
     * chessColor: 表示这个棋子的颜色，有红色，黑色，无色三种
     * isReversal: 表示是否翻转
     * selected: 表示这个棋子是否被选中
     */
    private ChessboardPoint chessboardPoint;
    protected final ChessColor chessColor;
    protected boolean isReversal;
    private boolean selected;

    /**
     * handle click event
     */
    private final ClickController clickController;

    //rank表示等级，General>Advisor>Minister>Chariot>Horse>Soldier
    //point表示分数， 30      10       5        5      5      1    Cannon:5
    private int rank;
    private int point;

    public int getRank() {
        return rank;
    }

    public int getPoint() {
        return point;
    }

    protected SquareComponent(ChessboardPoint chessboardPoint, Point location, ChessColor chessColor, ClickController clickController, int size) {
        enableEvents(AWTEvent.MOUSE_EVENT_MASK);
        setLocation(location);
        setSize(size, size);
        this.chessboardPoint = chessboardPoint;
        this.chessColor = chessColor;
        this.selected = false;
        this.clickController = clickController;
        this.isReversal = false;

        if (this instanceof GeneralChessComponent) {
            this.rank = 6;
            this.point = 30;
        }
        if (this instanceof AdvisorChessComponent) {
            this.rank = 5;
            this.point = 10;
        }
        if (this instanceof MinisterChessComponent) {
            this.rank = 4;
            this.point = 5;
        }
        if (this instanceof ChariotChessComponent) {
            this.rank = 3;
            this.point = 5;
        }
        if (this instanceof HorseChessComponent) {
            this.rank = 2;
            this.point = 5;
        }
        if (this instanceof SoldierChessComponent) {
            this.rank = 1;
            this.point = 1;
        }
        if (this instanceof EmptySlotComponent) {
            this.rank = 0;
            this.point = 0;
        }
        if (this instanceof CannonChessComponent) {
            this.rank = 2;
            this.point = 5;
        }


    }

    public boolean isReversal() {
        return isReversal;
    }

    public void setReversal(boolean reversal) {
        isReversal = reversal;
    }

    public static void setSpacingLength(int spacingLength) {
        SquareComponent.spacingLength = spacingLength;
    }

    public ChessboardPoint getChessboardPoint() {
        return chessboardPoint;
    }

    public void setChessboardPoint(ChessboardPoint chessboardPoint) {
        this.chessboardPoint = chessboardPoint;
    }

    public ChessColor getChessColor() {
        return chessColor;
    }

    public boolean isSelected() {
        return selected;
    }

    public void setSelected(boolean selected) {
        this.selected = selected;
    }


    /**
     * @param another 主要用于和另外一个棋子交换位置
     *                <br>
     *                调用时机是在移动棋子的时候，将操控的棋子和对应的空位置棋子(EmptySlotComponent)做交换
     */
    public void swapLocation(SquareComponent another) {
        ChessboardPoint chessboardPoint1 = getChessboardPoint(), chessboardPoint2 = another.getChessboardPoint();
        Point point1 = getLocation(), point2 = another.getLocation();
        setChessboardPoint(chessboardPoint2);
        setLocation(point2);
        another.setChessboardPoint(chessboardPoint1);
        another.setLocation(point1);
    }

    /**
     * @param e 响应鼠标监听事件
     *          <br>
     *          当接收到鼠标动作的时候，这个方法就会自动被调用，调用监听者的onClick方法，处理棋子的选中，移动等等行为。
     */
    @Override
    protected void processMouseEvent(MouseEvent e) {
        super.processMouseEvent(e);
        if (e.getID() == MouseEvent.MOUSE_PRESSED) {
            System.out.printf("Click [%d,%d]\n", chessboardPoint.getX(), chessboardPoint.getY());
            clickController.onClick(this);
        }
    }

    /**
     * @param chessboard  棋盘
     * @param destination 目标位置，如(0, 0), (0, 1)等等
     * @return this棋子对象的移动规则和当前位置(chessboardPoint)能否到达目标位置
     * <br>
     * 这个方法主要是检查移动的合法性，如果合法就返回true，反之是false。
     */
    //todo: Override this method for Cannon 已完成
    public boolean canMoveTo(SquareComponent[][] chessboard, ChessboardPoint destination) {
        SquareComponent destinationChess = chessboard[destination.getX()][destination.getY()];
        int x = this.getChessboardPoint().getX();
        int y = this.getChessboardPoint().getY();
        boolean isMoveValid = true;
        boolean isRankValid = false;
        if (!(this instanceof CannonChessComponent)) {
            if (!((Math.abs(x - destination.getX()) == 1 && y == destination.getY()) ||
                    (Math.abs(y - destination.getY()) == 1 && x == destination.getX()))) {
                isMoveValid = false;
            }
            if (!(this instanceof SoldierChessComponent)) {
                if (this.getRank() >= destinationChess.getRank()) isRankValid = true;
            } else {
                if (destinationChess instanceof GeneralChessComponent || destinationChess.getRank() <= 1)
                    isRankValid = true;
            }
        } else isRankValid = true;
        return (destinationChess.isReversal || destinationChess instanceof EmptySlotComponent) && isMoveValid && isRankValid;
        //todo: complete this method 已完成
    }


    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponents(g);
        System.out.printf("repaint chess [%d,%d]\n", chessboardPoint.getX(), chessboardPoint.getY());
        g.setColor(squareColor);
        g.fillRect(1, 1, this.getWidth() - 2, this.getHeight() - 2);
    }

}
