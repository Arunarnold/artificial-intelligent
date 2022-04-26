# artificial-intelligent
 
 ​import​ ​sys 
  
 ​#keeps best move values 
 ​class​ ​BestMove​: 
 ​        ​def​ ​__init__​(​self​,​row​: ​int​, ​col​: ​int​,​val​: ​int​): 
 ​                ​self​.​row​ ​=​ ​row 
 ​                ​self​.​col​ ​=​ ​col 
 ​                ​self​.​val​ ​=​ ​val 
  
 ​# check sudoku rules 
 ​def​ ​check_sudoku​(​grid​,​row​,​col​,​num​): 
 ​        ​#sub square selector 
 ​        ​subsquare_row​, ​subsquare_col​ ​=​ ​3​ ​*​(​row​//​3​), ​3​ ​*​(​col​//​3​) 
 ​        ​for​ ​i​ ​in​ ​range​(​subsquare_row​,​subsquare_row​+​3​): 
 ​                ​for​ ​j​ ​in​ ​range​(​subsquare_col​,​subsquare_col​+​3​): 
 ​                        ​if​ ​grid​[​i​][​j​] ​==​ ​num​: 
 ​                                ​return​ ​False 
 ​        ​for​ ​x​ ​in​ ​range​ (​9​): 
 ​                ​if​ ​grid​[​row​][​x​] ​==​ ​num​: 
 ​                        ​return​ ​False 
 ​                ​elif​ ​grid​[​x​][​col​] ​==​ ​num​: 
 ​                        ​return​ ​False 
 ​        ​return​ ​True 
  
 ​# evaluate the current pos 
 ​def​ ​evaluate​(​grid​): 
 ​        ​if​ ​locked​: 
 ​                ​if​ ​turn​==​1​: 
 ​                        ​return​ ​10 
 ​                ​else​: 
 ​                        ​return​ ​-​10 
 ​        ​for​ ​i​ ​in​ ​range​(​9​): 
 ​                ​for​ ​j​ ​in​ ​range​(​9​): 
 ​                        ​if​ ​grid​[​i​][​j​]​==​0​: 
 ​                                ​return​ ​-​1 
 ​        ​if​ ​turn​==​1​: 
 ​                ​return​ ​10 
 ​        ​else​: 
 ​                ​return​ ​-​10 
  
  
 ​def​ ​Pruning​(​locked​,​grid​,​turn​,​BestMove​,​alpha​,​beta​): 
 ​        ​if​(​turn​==​0​): 
 ​                ​bestVal​ ​=​ ​1000 
 ​                ​moveVal​=​1000 
 ​                ​BestMove​.​row​ ​=​ ​-​1 
 ​                ​BestMove​.​col​ ​=​ ​-​1 
 ​                ​BestMove​.​val​ ​=​ ​0 
  
 ​                ​for​ ​i​ ​in​ ​range​(​9​): 
 ​                        ​for​ ​j​ ​in​ ​range​(​9​): 
 ​                                ​# Check if cell is empty 
 ​                                ​if​ ​grid​[​i​][​j​]​==​0​ : 
 ​                                        ​for​ ​k​ ​in​ (​k​+​1​ ​for​ ​k​ ​in​ ​range​(​9​)): 
 ​                                                ​locked​=​False 
 ​                                                ​if​ ​check_sudoku​(​grid​,​i​,​j​,​k​): 
 ​                                                        ​# Make the move if valid for sudoku rules 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​k 
 ​                                                        ​bestVal​ ​=​ ​min​(​bestVal​, 
 ​                                                                ​Pruning​(​locked​,​grid​,​1​,​BestMove​,​alpha​,​beta​)[​0​]) 
  
 ​                                                        ​beta​ ​=​ ​min​(​beta​, ​bestVal​) 
  
 ​                                                        ​# Alpha Beta Pruning 
  
 ​                                                        ​if​ ​moveVal​ ​>​ ​bestVal​: 
 ​                                                                ​BestMove​.​row​ ​=​ ​i 
 ​                                                                ​BestMove​.​col​ ​=​ ​j 
 ​                                                                ​BestMove​.​val​ ​=​ ​k 
 ​                                                                ​bestVal​ ​=​ ​moveVal 
 ​                                                        ​if​ ​beta​ ​<=​ ​alpha​: 
 ​                                                                ​grid​[​i​][​j​] ​=​ ​0 
 ​                                                                ​break 
  
 ​                                                ​if​(​grid​[​i​][​j​] ​==​ ​0​): 
 ​                                                        ​locked​=​True 
 ​                                                ​else​: 
 ​                                                        ​#Undo the move 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​0 
  
 ​                                                 ​#If the value of the current move is 
 ​                                                ​#// more than the best valuwere, then update 
 ​                                                ​# best/ 
 ​                ​turn​=​1 
  
 ​                ​#assign the best 
 ​                ​if​ ​BestMove​.​row​==​-​1​ ​or​ ​BestMove​.​col​==​-​1​: 
 ​                        ​locked​=​True 
 ​                ​#maximizer 
 ​        ​else​: 
 ​                ​bestVal​ ​=​ ​-​1000 
 ​                ​moveVal​ ​=​-​1000 
 ​                ​BestMove​.​row​ ​=​ ​-​1 
 ​                ​BestMove​.​col​ ​=​ ​-​1 
 ​                ​BestMove​.​val​ ​=​ ​0 
 ​                ​for​ ​i​ ​in​ ​range​(​9​): 
 ​                        ​for​ ​j​ ​in​ ​range​(​9​): 
 ​                                        ​# Check if cell is empty 
 ​                                ​if​ ​grid​[​i​][​j​]​==​0​ : 
 ​                                        ​for​ ​k​ ​in​ (​k​+​1​ ​for​ ​k​ ​in​ ​range​(​9​)): 
 ​                                                ​locked​=​False 
 ​                                                ​if​ ​check_sudoku​(​grid​,​i​,​j​,​k​): 
 ​                                                        ​# Make the move 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​k 
 ​                                                        ​bestVal​ ​=​ ​max​( ​bestVal​, 
 ​                                                                ​Pruning​(​locked​,​grid​, ​0​,​BestMove​,​alpha​,​beta​)[​0​] ) 
 ​                                                        ​alpha​ ​=​ ​max​(​alpha​, ​bestVal​) 
  
  
 ​                                                        ​if​ ​moveVal​ ​<​ ​bestVal​: 
 ​                                                                ​BestMove​.​row​ ​=​ ​i 
 ​                                                                ​BestMove​.​col​ ​=​ ​j 
 ​                                                                ​BestMove​.​val​ ​=​ ​k 
 ​                                                                ​bestVal​ ​=​ ​moveVal 
 ​                                                        ​# Alpha Beta Pruning 
 ​                                                        ​if​ ​beta​ ​<=​ ​alpha​: 
 ​                                                                ​grid​[​i​][​j​] ​=​ ​0 
 ​                                                                ​break 
  
 ​                                                ​if​(​grid​[​i​][​j​] ​==​ ​0​): 
 ​                                                        ​locked​=​True 
 ​                                                ​else​: 
 ​                                                        ​#Undo the move 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​0 
  
 ​                ​turn​=​0 
  
 ​                ​if​ ​BestMove​.​row​==​-​1​ ​or​ ​BestMove​.​col​==​-​1​: 
 ​                        ​locked​=​True 
 ​        ​if​ ​locked​: 
 ​                ​moveVal​=​0 
 ​        ​return​ ​moveVal​,​turn​,​BestMove 
  
 ​def​ ​Minimax​(​locked​,​grid​,​turn​,​BestMove​): 
 ​        ​if​(​turn​==​0​): 
 ​                ​bestVal​ ​=​ ​1000 
 ​                ​moveVal​=​1000 
 ​                ​BestMove​.​row​ ​=​ ​-​1 
 ​                ​BestMove​.​col​ ​=​ ​-​1 
 ​                ​BestMove​.​val​ ​=​ ​0 
  
 ​                ​for​ ​i​ ​in​ ​range​(​9​): 
 ​                        ​for​ ​j​ ​in​ ​range​(​9​): 
 ​                                        ​# Check if cell is empty 
 ​                                ​if​ ​grid​[​i​][​j​]​==​0​ : 
 ​                                        ​for​ ​k​ ​in​ (​k​+​1​ ​for​ ​k​ ​in​ ​range​(​9​)): 
 ​                                                ​locked​=​False 
 ​                                                ​if​ ​check_sudoku​(​grid​,​i​,​j​,​k​): 
 ​                                                                        ​# Make the move 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​k 
 ​                                                        ​bestVal​ ​=​ ​min​(​bestVal​, 
 ​                                                                ​Minimax​(​locked​,​grid​,​1​,​BestMove​)[​0​]) 
 ​                                                        ​if​ ​moveVal​ ​>​ ​bestVal​: 
 ​                                                                ​BestMove​.​row​ ​=​ ​i 
 ​                                                                ​BestMove​.​col​ ​=​ ​j 
 ​                                                                ​BestMove​.​val​ ​=​ ​k 
 ​                                                                ​bestVal​ ​=​ ​moveVal 
  
 ​                                                ​if​(​grid​[​i​][​j​] ​==​ ​0​): 
 ​                                                        ​locked​=​True 
 ​                                                ​else​: 
 ​                                                                        ​#Undo the move 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​0 
  
  
 ​                ​turn​=​1 
  
 ​                ​if​ ​BestMove​.​row​==​-​1​ ​or​ ​BestMove​.​col​==​-​1​: 
 ​                        ​locked​=​True 
  
 ​                ​#maximizer 
 ​        ​else​: 
 ​                ​bestVal​ ​=​ ​-​1000 
 ​                ​moveVal​ ​=​-​1000 
 ​                ​BestMove​.​row​ ​=​ ​-​1 
 ​                ​BestMove​.​col​ ​=​ ​-​1 
 ​                ​BestMove​.​val​ ​=​ ​0 
 ​                ​for​ ​i​ ​in​ ​range​(​9​): 
 ​                        ​for​ ​j​ ​in​ ​range​(​9​): 
 ​                                        ​# Check if cell is empty 
 ​                                ​if​ ​grid​[​i​][​j​]​==​0​ : 
 ​                                        ​for​ ​k​ ​in​ (​k​+​1​ ​for​ ​k​ ​in​ ​range​(​9​)): 
 ​                                                ​locked​=​False 
 ​                                                ​if​ ​check_sudoku​(​grid​,​i​,​j​,​k​): 
 ​                                                ​# Make the move 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​k 
 ​                                                        ​bestVal​ ​=​ ​max​( ​bestVal​, 
 ​                                                                ​Minimax​(​locked​,​grid​, ​0​,​BestMove​)[​0​] ) 
 ​                                                        ​if​ ​moveVal​ ​<​ ​bestVal​: 
 ​                                                                ​BestMove​.​row​ ​=​ ​i 
 ​                                                                ​BestMove​.​col​ ​=​ ​j 
 ​                                                                ​BestMove​.​val​ ​=​ ​k 
 ​                                                                ​bestVal​ ​=​ ​moveVal 
  
 ​                                                ​if​(​grid​[​i​][​j​] ​==​ ​0​): 
 ​                                                        ​locked​=​True 
 ​                                                ​else​: 
 ​                                                                ​#Undo the move 
 ​                                                        ​grid​[​i​][​j​] ​=​ ​0 
  
 ​                ​turn​=​0 
  
 ​                ​if​ ​BestMove​.​row​==​-​1​ ​or​ ​BestMove​.​col​==​-​1​: 
 ​                        ​locked​=​True 
 ​        ​if​ ​locked​: 
 ​                ​moveVal​=​0 
 ​        ​return​ ​moveVal​,​turn​,​BestMove 
  
 ​def​ ​Selector​(​method​): 
  
 ​        ​method_name​ ​=​ { 
 ​                ​"1"​: ​Minimax​, 
 ​                ​"2"​: ​Pruning​, 
 ​        } 
 ​        ​ret​=​method_name​[​method​] 
  
 ​        ​return​ ​ret 
 ​def​ ​main​(): 
 ​        ​print​(​'Enter Your Choice:'​) 
 ​        ​print​(​'1 -> Minimax'​) 
 ​        ​print​(​'2 -> Pruning'​) 
 ​        ​global​ ​locked 
 ​        ​global​ ​turn 
 ​        ​locked​ ​=​ ​False 
 ​        ​turn​ ​=​1 
 ​        ​x​=​ ​input​() 
  
 ​        ​grid​ ​=​ [] 
 ​        ​RNum​=​0 
 ​        ​#read from txt 
 ​        ​with​ ​open​(​sys​.​argv​[​1​]) ​as​ ​arr​: 
 ​                ​for​ ​line​ ​in​ ​arr​: 
 ​                        ​row_grid​ ​=​ [] 
 ​                        ​CNum​=​0 
  
 ​                        ​for​ ​col_grid​ ​in​ ​line​.​split​(​" "​): 
 ​                                ​if​ ​CNum​>=​9​: 
 ​                                        ​break​; 
 ​                                ​temp​=​col_grid​.​rstrip​(​"​\n​"​) 
 ​                                ​row_grid​.​append​(​int​(​temp​)) 
 ​                                ​CNum​=​CNum​+​1 
 ​                        ​grid​.​append​(​row_grid​) 
 ​                        ​RNum​=​RNum​+​1 
  
 ​        ​# print not solved grid 
 ​        ​for​ ​row_grid​ ​in​ ​grid​: 
 ​                ​print​(​row_grid​) 
 ​        ​notlocked​=​True 
 ​        ​global​ ​BestMove 
 ​        ​BestMove​.​row​ ​=​ ​-​1 
 ​        ​BestMove​.​col​ ​=​ ​-​1 
 ​        ​BestMove​.​val​ ​=​ ​0 
 ​        ​if​(​Selector​(​x​)​==​Minimax​): 
 ​                ​# while grid has moveable bit 
 ​                ​while​(​notlocked​==​True​): 
 ​                        ​move​,​turn​,​BestMove​ ​=​ ​Selector​(​x​)(​locked​,​grid​,​turn​,​BestMove​) 
 ​                        ​notlocked​=​False 
 ​                        ​if​(​BestMove​.​val​!=​0​): 
 ​                                ​grid​[​BestMove​.​row​][​BestMove​.​col​] ​=​  ​BestMove​.​val 
 ​                        ​if​(​turn​==​1​): 
 ​                                ​print​(​"min oynadi"​) 
 ​                                ​for​ ​row_grid​ ​in​ ​grid​: 
 ​                                        ​print​(​row_grid​) 
 ​                        ​else​: 
 ​                                ​print​(​"max oynadi"​) 
 ​                                ​for​ ​row_grid​ ​in​ ​grid​: 
 ​                                        ​print​(​row_grid​) 
  
 ​                        ​for​ ​i​ ​in​ ​range​(​9​): 
 ​                                ​for​ ​j​ ​in​ ​range​(​9​): 
 ​                                        ​if​ ​grid​[​i​][​j​]​==​0​ : 
 ​                                                ​for​ ​k​ ​in​ (​k​+​1​ ​for​ ​k​ ​in​ ​range​(​9​)): 
 ​                                                        ​if​ ​check_sudoku​(​grid​,​i​,​j​,​k​): 
 ​                                                                ​notlocked​=​True 
 ​        ​else​: 
 ​                ​while​(​notlocked​==​True​): 
 ​                        ​move​,​turn​,​BestMove​ ​=​ ​Selector​(​x​)(​locked​,​grid​,​turn​,​BestMove​,​-​1000​,​1000​) 
 ​                        ​notlocked​=​False 
 ​                        ​if​(​BestMove​.​val​!=​0​): 
 ​                                ​grid​[​BestMove​.​row​][​BestMove​.​col​] ​=​  ​BestMove​.​val 
 ​                        ​if​(​turn​==​1​): 
 ​                                ​print​(​"min oynadi"​) 
 ​                                ​for​ ​row_grid​ ​in​ ​grid​: 
 ​                                        ​print​(​row_grid​) 
 ​                        ​else​: 
 ​                                ​print​(​"max oynadi"​) 
 ​                                ​for​ ​row_grid​ ​in​ ​grid​: 
 ​                                        ​print​(​row_grid​) 
 ​                        ​for​ ​i​ ​in​ ​range​(​9​): 
 ​                                ​for​ ​j​ ​in​ ​range​(​9​): 
 ​                                        ​if​ ​grid​[​i​][​j​]​==​0​ : 
 ​                                                ​for​ ​k​ ​in​ (​k​+​1​ ​for​ ​k​ ​in​ ​range​(​9​)): 
 ​                                                        ​if​ ​check_sudoku​(​grid​,​i​,​j​,​k​): 
 ​                                                                ​notlocked​=​True 
  
 ​        ​if​(​turn​==​1​): 
 ​                ​print​(​"Minimizer Won"​) 
 ​        ​else​: 
 ​                ​print​(​"Maximizer Won"​) 
 ​        ​for​ ​row_grid​ ​in​ ​grid​: 
 ​                ​print​(​row_grid​) 
  
  
  
 ​main​()
