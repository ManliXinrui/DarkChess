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
