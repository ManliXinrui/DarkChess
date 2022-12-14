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

package controller;


import chessComponent.CannonChessComponent;
import chessComponent.SquareComponent;
import chessComponent.EmptySlotComponent;
import model.ChessColor;
import view.ChessGameFrame;
import view.Chessboard;

public class ClickController {
    private final Chessboard chessboard;
    private SquareComponent first;

    public ClickController(Chessboard chessboard) {
        this.chessboard = chessboard;
    }

    public void onClick(SquareComponent squareComponent) {
        //判断第一次点击
        if (first == null) {
            if (handleFirst(squareComponent)) {
                squareComponent.setSelected(true);
                first = squareComponent;
                first.repaint();
            }
        } else {
            if (first == squareComponent) { // 再次点击取消选取
                squareComponent.setSelected(false);
                SquareComponent recordFirst = first;
                first = null;
                recordFirst.repaint();
            } else if (handleSecond(squareComponent)) {
                //repaint in swap chess method.
                chessboard.swapChessComponents(first, squareComponent);
                chessboard.clickController.swapPlayer();
                chessboard.clickController.updatePoints();

                first.setSelected(false);
                first = null;
            }
        }
    }


    /**
     * @param squareComponent 目标选取的棋子
     * @return 目标选取的棋子是否与棋盘记录的当前行棋方颜色相同
     */

    private boolean handleFirst(SquareComponent squareComponent) {
        if (chessboard.getBlackPoints() >= 60 || chessboard.getRedPoints() >= 60) {
            return false;
        }
        if (!squareComponent.isReversal()) {
            squareComponent.setReversal(true);
            System.out.printf("onClick to reverse a chess [%d,%d]\n", squareComponent.getChessboardPoint().getX(), squareComponent.getChessboardPoint().getY());
            squareComponent.repaint();
            if (ChessGameFrame.getStatusLabel().getText().equals("INITIAL PLAYER")) {
                chessboard.clickController.chooseInitialPlayer(chessboard.getChessComponents(), squareComponent);
                chessboard.setCurrentColor(chessboard.getCurrentColor() == ChessColor.BLACK ? ChessColor.RED : ChessColor.BLACK);
            } else
                chessboard.clickController.swapPlayer();
            chessboard.clickController.updatePoints();
            return false;
        }
        return squareComponent.getChessColor() == chessboard.getCurrentColor();
    }

    /**
     * @param squareComponent first棋子目标移动到的棋子second
     * @return first棋子是否能够移动到second棋子位置
     */

    private boolean handleSecond(SquareComponent squareComponent) {
        System.out.println(squareComponent.getName());
        if (chessboard.getBlackPoints() >= 60 || chessboard.getRedPoints() >= 60) {
            return false;
        }
        //炮可以吃没翻开的棋子
        if (first instanceof CannonChessComponent) {
            if (!squareComponent.isReversal()) {
                if (!(squareComponent instanceof EmptySlotComponent)) {
                    //炮吃的子是什么颜色，就给相反颜色加分
                    if (squareComponent.getChessColor() == ChessColor.BLACK) {
                        chessboard.setRedPoints(squareComponent.getPoint());
                        ChessGameFrame.getRedHasEatenLabel().setText(ChessGameFrame.getRedHasEatenLabel().getText()+" "+squareComponent.getName());
                    } else {
                        chessboard.setBlackPoints(squareComponent.getPoint());
                        ChessGameFrame.getBlackHasEatenLabel().setText(ChessGameFrame.getBlackHasEatenLabel().getText()+" "+squareComponent.getName());
                    }
                    return first.canMoveTo(chessboard.getChessComponents(), squareComponent.getChessboardPoint());
                }
            }
        }//
        //没翻开或空棋子，进入if
        if (!squareComponent.isReversal()) {
            //没翻开且非空棋子不能走
            if (!(squareComponent instanceof EmptySlotComponent)) {
                return false;
            }
        }
        boolean isValid = squareComponent.getChessColor() != chessboard.getCurrentColor() &&
                first.canMoveTo(chessboard.getChessComponents(), squareComponent.getChessboardPoint());
        if (isValid) {
            if (squareComponent.getChessColor() == ChessColor.BLACK) {
                chessboard.setRedPoints(squareComponent.getPoint());
                ChessGameFrame.getRedHasEatenLabel().setText(ChessGameFrame.getRedHasEatenLabel().getText()+" "+squareComponent.getName());
            } else {
                chessboard.setBlackPoints(squareComponent.getPoint());
                ChessGameFrame.getBlackHasEatenLabel().setText(ChessGameFrame.getBlackHasEatenLabel().getText()+" "+squareComponent.getName());
            }
        }
        return isValid;
    }

    public void swapPlayer() {
        chessboard.setCurrentColor(chessboard.getCurrentColor() == ChessColor.BLACK ? ChessColor.RED : ChessColor.BLACK);
        ChessGameFrame.getStatusLabel().setText(String.format("%s's TURN", chessboard.getCurrentColor().getName()));
    }

    public void updatePoints() {
        ChessGameFrame.getBlackPointsLabel().setText(String.format("BLACK's POINTS: %d", chessboard.getBlackPoints()));
        ChessGameFrame.getRedPointsLabel().setText(String.format("RED's POINTS: %d", chessboard.getRedPoints()));
        if (chessboard.getBlackPoints() >= 60 || chessboard.getRedPoints() >= 60) {
            ChessGameFrame.getStatusLabel0().setText(String.format("END! %s WIN!", chessboard.getRedPoints() >= 60 ? "RED" : "BLACK"));
        }
    }

    public void chooseInitialPlayer(SquareComponent[][] allChess, SquareComponent firstSquareComponent) {
        int counter = 0;
        for (int i = 0; i < allChess.length; i++) {
            for (int j = 0; j < allChess[i].length; j++) {
                if (allChess[i][j].isReversal()) counter++;
            }
        }
        if (counter == 1) {
            System.out.printf("The initial player is %s", firstSquareComponent.getChessColor().getName());
            if (firstSquareComponent.getChessColor() == ChessColor.RED) {
                chessboard.setCurrentColor(ChessColor.RED);
                ChessGameFrame.getStatusLabel().setText(String.format("BLACK's TURN"));
            } else {
                chessboard.setCurrentColor(ChessColor.BLACK);
                ChessGameFrame.getStatusLabel().setText(String.format("RED's TURN"));
            }
        }
    }
}

package controller;

import view.Chessboard;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.List;

/**
 * 这个类主要完成由窗体上组件触发的动作。
 * 例如点击button等
 * ChessGameFrame中组件调用本类的对象，在本类中的方法里完成逻辑运算，将运算的结果传递至chessboard中绘制
 */
public class GameController {
    private Chessboard chessboard;
    public Chessboard getChessboard() {
        return chessboard;
    }


    public GameController(Chessboard chessboard) {
        this.chessboard = chessboard;
    }


    public List<String> loadGameFromFile(String path) {
        try {
            List<String> chessData = Files.readAllLines(Path.of(path));
            chessboard.loadGame(chessData);
            return chessData;
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }

}

package model;

/**
 * 这个类表示棋盘上的位置，如(0, 0), (0, 3)等等
 * 其中，左上角是(0, 0)，左下角是(7, 0)，右上角是(0, 3)，右下角是(7, 3)
 */
public class ChessboardPoint {
    private int x, y;

    /**
     *
     * @param x: row
     * @param y: col
     */
    public ChessboardPoint(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }

    @Override
    public String toString() {
        return "("+x + ","+y+") " + "on the chessboard is clicked!";
    }
}

package model;

import java.awt.*;

/**
 * 这个类主要用于包装Color对象，用于Chess游戏使用。
 */
public enum ChessColor {
    BLACK("Black", Color.BLACK), RED("RED", Color.RED), NONE("No Player", Color.WHITE);

    private final String name;
    private final Color color;

    ChessColor(String name, Color color) {
        this.name = name;
        this.color = color;
    }

    public String getName() {
        return name;
    }

    public Color getColor() {
        return color;
    }
}

package view;


import chessComponent.*;
import model.*;
import controller.ClickController;

import javax.swing.*;
import java.awt.*;
import java.util.List;
import java.util.Random;

/**
 * 这个类表示棋盘组建，其包含：
 * SquareComponent[][]: 4*8个方块格子组件
 */
public class Chessboard extends JComponent {


    private static final int ROW_SIZE = 8;
    private static final int COL_SIZE = 4;

    private final SquareComponent[][] squareComponents = new SquareComponent[ROW_SIZE][COL_SIZE];
    //todo: you can change the initial player
    private ChessColor currentColor = ChessColor.BLACK;

    //all chessComponents in this chessboard are shared only one model controller
    public final ClickController clickController = new ClickController(this);
    private final int CHESS_SIZE;

    public int blackPoints = 0;
    public int redPoints = 0;

    public int getBlackPoints() {
        return blackPoints;
    }

    public void setBlackPoints(int blackPoints) {
        this.blackPoints += blackPoints;
    }

    public int getRedPoints() {
        return redPoints;
    }

    public void setRedPoints(int redPoints) {
        this.redPoints += redPoints;
    }

    public Chessboard(int width, int height) {
        setLayout(null); // Use absolute layout.
        setSize(width + 2, height);
        CHESS_SIZE = (height - 6) / 8;
        SquareComponent.setSpacingLength(CHESS_SIZE / 12);
        System.out.printf("chessboard [%d * %d], chess size = %d\n", width, height, CHESS_SIZE);

        initAllChessOnBoard();
    }

    public SquareComponent[][] getChessComponents() {
        return squareComponents;
    }

    public ChessColor getCurrentColor() {
        return currentColor;
    }

    public void setCurrentColor(ChessColor currentColor) {
        this.currentColor = currentColor;
    }

    /**
     * 将SquareComponent 放置在 ChessBoard上。里面包含移除原有的component及放置新的component
     *
     * @param squareComponent
     */
    public void putChessOnBoard(SquareComponent squareComponent) {
        int row = squareComponent.getChessboardPoint().getX(), col = squareComponent.getChessboardPoint().getY();
        if (squareComponents[row][col] != null) {
            remove(squareComponents[row][col]);
        }
        add(squareComponents[row][col] = squareComponent);
        repaint();
    }

    /**
     * 交换chess1 chess2的位置
     *
     * @param chess1
     * @param chess2
     */
    public void swapChessComponents(SquareComponent chess1, SquareComponent chess2) {
        // Note that chess1 has higher priority, 'destroys' chess2 if exists.
        if (!(chess2 instanceof EmptySlotComponent)) {
            remove(chess2);
            add(chess2 = new EmptySlotComponent(chess2.getChessboardPoint(), chess2.getLocation(), clickController, CHESS_SIZE));
        }
        chess1.swapLocation(chess2);
        int row1 = chess1.getChessboardPoint().getX(), col1 = chess1.getChessboardPoint().getY();
        squareComponents[row1][col1] = chess1;
        int row2 = chess2.getChessboardPoint().getX(), col2 = chess2.getChessboardPoint().getY();
        squareComponents[row2][col2] = chess2;

        //只重新绘制chess1 chess2，其他不变
        chess1.repaint();
        chess2.repaint();
    }


    //FIXME:   Initialize chessboard for testing only.
    public void initAllChessOnBoard() {
        Random random = new Random();
        //生成32个棋子。
        int[] arr = new int[32];
        for (int i = 0; i < arr.length; i++) {
            arr[i] = random.nextInt(32);
            for (int j = 0; j < i; j++) {
                if (arr[i] == arr[j]) {
                    i--;
                    break;
                }
            }
        }
        int k = 0;
        for (int i = 0; i < squareComponents.length; i++) {
            for (int j = 0; j < squareComponents[i].length; j++) {
                //ChessColor color = random.nextInt(2) == 0 ? ChessColor.RED : ChessColor.BLACK;
                SquareComponent squareComponent;
                switch (arr[k]) {
                    case 0:
                        squareComponent = new GeneralChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.RED, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 1:
                        squareComponent = new GeneralChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.BLACK, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 2:
                    case 4:
                        squareComponent = new AdvisorChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.RED, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 3:
                    case 5:
                        squareComponent = new AdvisorChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.BLACK, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 6:
                    case 8:
                        squareComponent = new MinisterChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.RED, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 7:
                    case 9:
                        squareComponent = new MinisterChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.BLACK, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 10:
                    case 12:
                        squareComponent = new ChariotChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.RED, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 11:
                    case 13:
                        squareComponent = new ChariotChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.BLACK, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 14:
                    case 16:
                        squareComponent = new HorseChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.RED, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 15:
                    case 17:
                        squareComponent = new HorseChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.BLACK, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 18:
                    case 20:
                    case 22:
                    case 24:
                    case 26:
                        squareComponent = new SoldierChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.RED, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 19:
                    case 21:
                    case 23:
                    case 25:
                    case 27:
                        squareComponent = new SoldierChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.BLACK, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 28:
                    case 30:
                        squareComponent = new CannonChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.RED, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                    case 29:
                    case 31:
                        squareComponent = new CannonChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), ChessColor.BLACK, clickController, CHESS_SIZE);
                        squareComponent.setVisible(true);
                        putChessOnBoard(squareComponent);
                        k++;
                        break;
                }
            }
                /*if (random.nextInt(2) == 0) {
                    squareComponent = new ChariotChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), color, clickController, CHESS_SIZE);
                } else {
                    squareComponent = new SoldierChessComponent(new ChessboardPoint(i, j), calculatePoint(i, j), color, clickController, CHESS_SIZE);
                }
                squareComponent.setVisible(true);
                putChessOnBoard(squareComponent);*/
        }
    }


    /**
     * 绘制棋盘格子
     *
     * @param g
     */
    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        g.fillRect(0, 0, this.getWidth(), this.getHeight());
        ((Graphics2D) g).setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
    }

    /**
     * 将棋盘上行列坐标映射成Swing组件的Point
     *
     * @param row 棋盘上的行
     * @param col 棋盘上的列
     * @return
     */
    private Point calculatePoint(int row, int col) {
        return new Point(col * CHESS_SIZE + 3, row * CHESS_SIZE + 3);
    }

    /**
     * 通过GameController调用该方法
     *
     * @param chessData
     */
    public void loadGame(List<String> chessData) {
        chessData.forEach(System.out::println);
    }
}

package view;

import controller.GameController;
import model.ChessColor;

import javax.swing.*;
import java.awt.*;

/**
 * 这个类表示游戏窗体，窗体上包含：
 * 1 Chessboard: 棋盘
 * 2 JLabel:  标签
 * 3 JButton： 按钮
 */
public class ChessGameFrame extends JFrame {
    private final int WIDTH;
    private final int HEIGHT;
    public final int CHESSBOARD_SIZE;
    private GameController gameController;
    private static JLabel statusLabel;
    private static JLabel statusLabel0;// in progress or end
    private static JLabel blackPointsLabel;
    private static JLabel redPointsLabel;
    private static JLabel blackHasEatenLabel;
    private static JLabel redHasEatenLabel;
    protected static boolean click = false;


    public ChessGameFrame(int width, int height) {
        setTitle("2022 CS109 Project Demo"); //设置标题
        this.WIDTH = width;
        this.HEIGHT = height;
        this.CHESSBOARD_SIZE = HEIGHT * 4 / 5;

        setSize(WIDTH, HEIGHT);
        setLocationRelativeTo(null); // Center the window.
        getContentPane().setBackground(Color.WHITE);
        setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE); //设置程序关闭按键，如果点击右上方的叉就游戏全部关闭了
        setLayout(null);

        addChessboard();
        addLabel();
        addHelloButton();
        addLoadButton();
        addRestartButton();
    }


    /**
     * 在游戏窗体中添加棋盘
     */
    private void addChessboard() {
        Chessboard chessboard = new Chessboard(CHESSBOARD_SIZE / 2, CHESSBOARD_SIZE);
        gameController = new GameController(chessboard);
        chessboard.setLocation(HEIGHT / 5, HEIGHT / 10);
        add(chessboard);
    }


    /**
     * 在游戏窗体中添加标签
     */
    private void addLabel() {
        statusLabel = new JLabel("INITIAL PLAYER");
        statusLabel.setLocation(WIDTH * 13 / 20, HEIGHT / 10);
        statusLabel.setSize(200, 60);
        statusLabel.setFont(new Font("Rockwell", Font.BOLD, 18));
        add(statusLabel);

        statusLabel0 = new JLabel("IN PROGRESS:");
        statusLabel0.setLocation(WIDTH * 13 / 20, HEIGHT / 10 - 30);
        statusLabel0.setSize(200, 60);
        statusLabel0.setFont(new Font("Rockwell", Font.BOLD, 20));
        statusLabel0.setForeground(Color.PINK);
        add(statusLabel0);

        blackPointsLabel = new JLabel("BLACK's POINTS: 0");
        blackPointsLabel.setLocation(WIDTH * 13 / 20, HEIGHT / 10 + 30);
        blackPointsLabel.setSize(200, 60);
        blackPointsLabel.setFont(new Font("Rockwell", Font.BOLD, 18));
        blackPointsLabel.setForeground(Color.GRAY);
        add(blackPointsLabel);

        redPointsLabel = new JLabel("RED's POINTS: 0");
        redPointsLabel.setLocation(WIDTH * 13 / 20, HEIGHT / 10 + 60);
        redPointsLabel.setSize(200, 60);
        redPointsLabel.setFont(new Font("Rockwell", Font.BOLD, 18));
        redPointsLabel.setForeground(Color.GRAY);
        add(redPointsLabel);

        blackHasEatenLabel = new JLabel("Black Player has eaten: ");
        blackHasEatenLabel.setLocation(WIDTH / 20 - 10, HEIGHT / 10 - 60);
        blackHasEatenLabel.setSize(2000, 20);
        blackHasEatenLabel.setFont(new Font("黑体", Font.BOLD, 18));
        blackHasEatenLabel.setForeground(Color.BLACK);
        add(blackHasEatenLabel);

        redHasEatenLabel = new JLabel("Red Player has eaten: ");
        redHasEatenLabel.setLocation(WIDTH / 20 - 10, HEIGHT / 10 - 30);
        redHasEatenLabel.setSize(2000, 20);
        redHasEatenLabel.setFont(new Font("黑体", Font.BOLD, 18));
        redHasEatenLabel.setForeground(Color.BLACK);
        add(redHasEatenLabel);
    }

    public static JLabel getStatusLabel() {
        return statusLabel;
    }

    public static JLabel getStatusLabel0() {
        return statusLabel0;
    }

    public static JLabel getBlackPointsLabel() {
        return blackPointsLabel;
    }

    public static JLabel getRedPointsLabel() {
        return redPointsLabel;
    }

    public static JLabel getBlackHasEatenLabel() {
        return blackHasEatenLabel;
    }

    public static JLabel getRedHasEatenLabel() {
        return redHasEatenLabel;
    }

    /**
     * 在游戏窗体中增加一个按钮，如果按下的话就会显示Hello, world!
     */

    private void addHelloButton() {
        JButton button = new JButton("Show Hello Here");
        button.addActionListener((e) -> JOptionPane.showMessageDialog(this, "Hello, world!"));
        button.setLocation(WIDTH * 13 / 20, HEIGHT / 10 + 120);
        button.setSize(180, 60);
        button.setFont(new Font("Rockwell", Font.BOLD, 20));
        add(button);
    }


    private void addLoadButton() {
        JButton button = new JButton("Load");
        button.setLocation(WIDTH * 13 / 20, HEIGHT / 10 + 360);
        button.setSize(180, 60);
        button.setFont(new Font("Rockwell", Font.BOLD, 20));
        button.setBackground(Color.LIGHT_GRAY);
        add(button);

        button.addActionListener(e -> {
            System.out.println("Click load");
            String path = JOptionPane.showInputDialog(this, "Input Path here");
            gameController.loadGameFromFile(path);
        });
    }

    private void addRestartButton() {
        JButton button = new JButton("Restart");
        button.setLocation(WIDTH * 13 / 20, HEIGHT / 10 + 240);
        button.setSize(180, 60);
        button.setFont(new Font("Rockwell", Font.BOLD, 20));
        add(button);
        button.addActionListener((e) -> {
            System.out.println("Click restart");
            gameController.getChessboard().initAllChessOnBoard();
            gameController.getChessboard().blackPoints = 0;
            gameController.getChessboard().redPoints = 0;
            gameController.getChessboard().clickController.updatePoints();
            ChessGameFrame.getStatusLabel().setText(String.format("INITIAL PLAYER"));
            click = true;
        });
    }
}
