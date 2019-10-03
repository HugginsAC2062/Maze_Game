# Maze_Game
import java.util.*;
import java.lang.Math;

class Main {
  public static int playerX = 0;
  public static int playerY = 0;

  public static void main(String[] args) {
    Scanner in = new Scanner(System.in);
    int[] walls = new int[10]; //states where the space is in each wall section

    for(int i = 0; i < 10; i++){
      walls[i] = randomNum(0, 9);
    }

    System.out.println("Hello! Welcome to the Maze Game. You are represented by the '*' character. When you are ready\nto begin, type \"READY\" or \"START\"");

    String start = in.nextLine();

    
    while(true){
      if((start.equals("R")) || (start.equals("S")) || (start.equals("START")) || (start.equals("READY"))){
        runGame(walls);
        int gameFinish = checkGameFinish();
        
        if(gameFinish == 1){
          System.out.println();
          System.out.println("You Win! Good job, I guess!");
          break;
        }

        playerMove(in, walls);

        if((playerX == -1) || (playerY == -1)){
          System.out.println();
          System.out.println("YOU RAN INTO A WALL");
          System.out.println("YOU DIED");
          break;
        }

      }else{
        System.out.println("When you are ready to begin, type\"READY\" or \"START\"");
        start = in.nextLine();
      }
    }
  }

  //GAME METHODS
  public static void runGame(int[] walls){
    for(int i = 0; i < 40; i++){
      System.out.print("-");
    }
    
    for(int row = 0; row < 10; row++){
      System.out.println();

      for(int column = 0; column < 10; column++){
        spaces(row, column);

        if(walls[column] == row){
          System.out.print(" ");
        }else{
          System.out.print("|");
        }
      }
    }

    System.out.println();
    for(int i = 0; i < 40; i++){
      System.out.print("-");
    }
  }

  public static int checkGameFinish(){
    int gameFinish = 0;

    if((playerX > 10)){
      gameFinish = 1;
    }
    return gameFinish;
  }

  public static void spaces(int row, int column){
    if((playerY == row) && (playerX == column)){
      System.out.print(" * ");
    }else{
      System.out.print("   ");
    }
  }

  public static void playerMove(Scanner in, int[] walls){
    System.out.println();
    System.out.println("COMMAND LIST (case sensitive): 'UP' goes up one space, 'DOWN' goes");
    System.out.println("down one space, 'GO' moves to next column (sideways)");
    System.out.println("MOVE: ");
    String move = in.nextLine();

    if(move.equals("UP")){
      if(playerY != 0){
        playerY--;
      }else{
        playerY = -1;
      }
    }else if(move.equals("DOWN")){
      if(playerY != 9){
        playerY++;
      }else{
        playerY = -1;
      }
    }else if(move.equals("GO")){
      if(playerY == walls[playerX]){
        playerX++;
      }else{
        playerX = -1;
      }
    }else if(move.equals("FLUPPING UP")){
      playerY = 0;
    }else if(move.equals("DOWN DAM IT")){
      playerY = 9;
    }else if(move.equals("CHUCK NORRIS")){
      playerX = 15; 
      playerY = 9;
    }
  }

  //Random Number Generator
  public static int randomNum(int min, int max){
    double random = Math.random();
    int randomNum = (int)((random * ((max - min) + 1)) + min);

    return randomNum;
  }
}
