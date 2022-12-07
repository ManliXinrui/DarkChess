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
