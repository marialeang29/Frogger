# Frogger
GitHub de Frogger 
# Se reconoce que el Frogger tiene un alto número de componentes por lo que a continuación se pondrán las diferentes las páginas del código  y sus comentarios respectivos. 
# BB_SYSTEM
/#	G0B1T: HDL EXAMPLES. 2018.
//######################################################################
//# Copyright (C) 2018. F.E.Segura-Quijano (FES) fsegura@uniandes.edu.co
//# 
//# This program is free software: you can redistribute it and/or modify
//# it under the terms of the GNU General Public License as published by
//# the Free Software Foundation, version 3 of the License.
//#
//# This program is distributed in the hope that it will be useful,
//# but WITHOUT ANY WARRANTY; without even the implied warranty of
//# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
//# GNU General Public License for more details.
//#
//# You should have received a copy of the GNU General Public License
//# along with this program.  If not, see <http://www.gnu.org/licenses/>
//####################################################################*/
# Ejemplo Original
//=======================================================
//  MODULE Definition
//=======================================================
module BB_SYSTEM (
//////////// OUTPUTS //////////
	BB_SYSTEM_display_OutBUS,
	BB_SYSTEM_max7219DIN_Out,
	BB_SYSTEM_max7219NCS_Out,
	BB_SYSTEM_max7219CLK_Out,

	BB_SYSTEM_startButton_Out, 
	BB_SYSTEM_upButton_Out,
	BB_SYSTEM_downButton_Out,
	BB_SYSTEM_leftButton_Out,
	BB_SYSTEM_rightButton_Out,
	BB_SYSTEM_TEST0,
	BB_SYSTEM_TEST1,
	BB_SYSTEM_TEST2,

//////////// INPUTS //////////
	BB_SYSTEM_CLOCK_50,
	BB_SYSTEM_RESET_InHigh,
	BB_SYSTEM_startButton_InLow, 
	BB_SYSTEM_upButton_InLow,
	BB_SYSTEM_downButton_InLow,
	BB_SYSTEM_leftButton_InLow,
	BB_SYSTEM_rightButton_InLow
);
//=======================================================
//  PARAMETER declarations
//=======================================================
 parameter DATAWIDTH_BUS = 8;
 parameter PRESCALER_DATAWIDTH = 23;
 parameter DISPLAY_DATAWIDTH = 12;
 
 parameter DATA_FIXED_INITREGPOINT_7 = 8'b00000000;
 parameter DATA_FIXED_INITREGPOINT_6 = 8'b00000000;
 parameter DATA_FIXED_INITREGPOINT_5 = 8'b00000000;
 parameter DATA_FIXED_INITREGPOINT_4 = 8'b00000000;
 parameter DATA_FIXED_INITREGPOINT_3 = 8'b00000000;
 parameter DATA_FIXED_INITREGPOINT_2 = 8'b00000000;
 parameter DATA_FIXED_INITREGPOINT_1 = 8'b00000000;
 parameter DATA_FIXED_INITREGPOINT_0 = 8'b01000000;
 
 parameter DATA_FIXED_INITREGBACKG_7 = 8'b10111101;
 parameter DATA_FIXED_INITREGBACKG_6 = 8'b00000000;
 parameter DATA_FIXED_INITREGBACKG_5 = 8'b00000000;
 parameter DATA_FIXED_INITREGBACKG_4 = 8'b00100000;
 parameter DATA_FIXED_INITREGBACKG_3 = 8'b00000000;
 parameter DATA_FIXED_INITREGBACKG_2 = 8'b00100000;
 parameter DATA_FIXED_INITREGBACKG_1 = 8'b00000000;
 parameter DATA_FIXED_INITREGBACKG_0 = 8'b00000000;
  
//=======================================================
//  PORT declarations
//=======================================================
output		[DISPLAY_DATAWIDTH-1:0] BB_SYSTEM_display_OutBUS;

output		BB_SYSTEM_max7219DIN_Out;
output		BB_SYSTEM_max7219NCS_Out;
output		BB_SYSTEM_max7219CLK_Out;

output 		BB_SYSTEM_startButton_Out;
output 		BB_SYSTEM_upButton_Out;
output 		BB_SYSTEM_downButton_Out;
output 		BB_SYSTEM_leftButton_Out;
output 		BB_SYSTEM_rightButton_Out;
output 		BB_SYSTEM_TEST0;
output 		BB_SYSTEM_TEST1;
output 		BB_SYSTEM_TEST2;

input		BB_SYSTEM_CLOCK_50;
input		BB_SYSTEM_RESET_InHigh;
input		BB_SYSTEM_startButton_InLow;
input		BB_SYSTEM_upButton_InLow;
input		BB_SYSTEM_downButton_InLow;
input		BB_SYSTEM_leftButton_InLow;
input		BB_SYSTEM_rightButton_InLow;
//=======================================================
//  REG/WIRE declarations
//=======================================================
// BUTTONs
wire 	BB_SYSTEM_startButton_InLow_cwire;
wire 	BB_SYSTEM_upButton_InLow_cwire;
wire 	BB_SYSTEM_downButton_InLow_cwire;
wire 	BB_SYSTEM_leftButton_InLow_cwire;
wire 	BB_SYSTEM_rightButton_InLow_cwire;

//POINT
wire	STATEMACHINEPOINT_clear_cwire;
wire	STATEMACHINEPOINT_load0_cwire;
wire	STATEMACHINEPOINT_load1_cwire;
wire	[1:0] STATEMACHINEPOINT_shiftselection_cwire;

wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data7_Out;
wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data6_Out;
wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data5_Out;
wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data4_Out;
wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data3_Out;
wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data2_Out;
wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data1_Out;
wire [DATAWIDTH_BUS-1:0] RegPOINTTYPE_2_POINTMATRIX_data0_Out;

//BACKGROUNG
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data7_Out;
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data6_Out;
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data5_Out;
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data4_Out;
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data3_Out;
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data2_Out;
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data1_Out;
wire [DATAWIDTH_BUS-1:0] RegBACKGTYPE_2_BACKGMATRIX_data0_Out;

wire [PRESCALER_DATAWIDTH-1:0] upSPEEDCOUNTER_data_BUS_wire;
wire SPEEDCOMPARATOR_2_STATEMACHINEBACKG_T0_cwire;
wire STATEMACHINEBACKG_clear_cwire;
wire STATEMACHINEBACKG_load_cwire;
wire [1:0] STATEMACHINEBACKG_shiftselection_cwire;
wire STATEMACHINEBACKG_upcount_cwire;

//BOTTOMSIDE COMPARATOR
wire BOTTOMSIDECOMPARATOR_2_STATEMACHINEBACKG_bottomside_cwire;

// GAME
wire [DATAWIDTH_BUS-1:0] regGAME_data7_wire;
wire [DATAWIDTH_BUS-1:0] regGAME_data6_wire;
wire [DATAWIDTH_BUS-1:0] regGAME_data5_wire;
wire [DATAWIDTH_BUS-1:0] regGAME_data4_wire;
wire [DATAWIDTH_BUS-1:0] regGAME_data3_wire;
wire [DATAWIDTH_BUS-1:0] regGAME_data2_wire;
wire [DATAWIDTH_BUS-1:0] regGAME_data1_wire;
wire [DATAWIDTH_BUS-1:0] regGAME_data0_wire;

wire 	[7:0] data_max;
wire 	[2:0] add;

wire [DATAWIDTH_BUS-1:0] upCOUNTER_2_BIN2BCD1_data_BUS_wire;
wire [DISPLAY_DATAWIDTH-1:0] BIN2BCD1_2_SEVENSEG1_data_BUS_wire;

//=======================================================
//  Structural coding
//=======================================================

//######################################################################
//#	INPUTS
//######################################################################
SC_DEBOUNCE1 SC_DEBOUNCE1_u0 (
// port map - connection between master ports and signals/registers   
	.SC_DEBOUNCE1_button_Out(BB_SYSTEM_startButton_InLow_cwire),
	.SC_DEBOUNCE1_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_DEBOUNCE1_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_DEBOUNCE1_button_In(~BB_SYSTEM_startButton_InLow)
);
SC_DEBOUNCE1 SC_DEBOUNCE1_u1 (
// port map - connection between master ports and signals/registers   
	.SC_DEBOUNCE1_button_Out(BB_SYSTEM_upButton_InLow_cwire),
	.SC_DEBOUNCE1_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_DEBOUNCE1_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_DEBOUNCE1_button_In(~BB_SYSTEM_upButton_InLow)
);
SC_DEBOUNCE1 SC_DEBOUNCE1_u2 (
// port map - connection between master ports and signals/registers   
	.SC_DEBOUNCE1_button_Out(BB_SYSTEM_downButton_InLow_cwire),
	.SC_DEBOUNCE1_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_DEBOUNCE1_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_DEBOUNCE1_button_In(~BB_SYSTEM_downButton_InLow)
);
SC_DEBOUNCE1 SC_DEBOUNCE1_u3 (
// port map - connection between master ports and signals/registers   
	.SC_DEBOUNCE1_button_Out(BB_SYSTEM_leftButton_InLow_cwire),
	.SC_DEBOUNCE1_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_DEBOUNCE1_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_DEBOUNCE1_button_In(~BB_SYSTEM_leftButton_InLow)
);
SC_DEBOUNCE1 SC_DEBOUNCE1_u4 (
// port map - connection between master ports and signals/registers   
	.SC_DEBOUNCE1_button_Out(BB_SYSTEM_rightButton_InLow_cwire),
	.SC_DEBOUNCE1_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_DEBOUNCE1_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_DEBOUNCE1_button_In(~BB_SYSTEM_rightButton_InLow)
);

//######################################################################
//#	POINT
//######################################################################
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_7)) SC_RegPOINTTYPE_u7 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data7_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data6_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data0_Out)
);
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_6)) SC_RegPOINTTYPE_u6 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data6_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data5_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data7_Out)
);
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_5)) SC_RegPOINTTYPE_u5 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data5_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data4_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data6_Out)
);
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_4)) SC_RegPOINTTYPE_u4 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data4_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data3_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data5_Out)
);
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_3)) SC_RegPOINTTYPE_u3 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data3_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data2_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data4_Out)
);
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_2)) SC_RegPOINTTYPE_u2 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data2_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data1_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data3_Out)
);
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_1)) SC_RegPOINTTYPE_u1 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data1_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data0_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data2_Out)
);
SC_RegPOINTTYPE #(.RegPOINTTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGPOINT(DATA_FIXED_INITREGPOINT_0)) SC_RegPOINTTYPE_u0 (
// port map - connection between master ports and signals/registers   
	.SC_RegPOINTTYPE_data_OutBUS(RegPOINTTYPE_2_POINTMATRIX_data0_Out),
	.SC_RegPOINTTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegPOINTTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegPOINTTYPE_clear_InLow(STATEMACHINEPOINT_clear_cwire),
	.SC_RegPOINTTYPE_load0_InLow(STATEMACHINEPOINT_load0_cwire),
	.SC_RegPOINTTYPE_load1_InLow(STATEMACHINEPOINT_load1_cwire),
	.SC_RegPOINTTYPE_shiftselection_In(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_RegPOINTTYPE_data0_InBUS(RegPOINTTYPE_2_POINTMATRIX_data7_Out),
	.SC_RegPOINTTYPE_data1_InBUS(RegPOINTTYPE_2_POINTMATRIX_data1_Out)
);

SC_STATEMACHINEPOINT SC_STATEMACHINEPOINT_u0 (
// port map - connection between master ports and signals/registers   
	.SC_STATEMACHINEPOINT_clear_OutLow(STATEMACHINEPOINT_clear_cwire), 
	.SC_STATEMACHINEPOINT_load0_OutLow(STATEMACHINEPOINT_load0_cwire),
	.SC_STATEMACHINEPOINT_load1_OutLow(STATEMACHINEPOINT_load1_cwire), 
	.SC_STATEMACHINEPOINT_shiftselection_Out(STATEMACHINEPOINT_shiftselection_cwire),
	.SC_STATEMACHINEPOINT_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_STATEMACHINEPOINT_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_STATEMACHINEPOINT_startButton_InLow(BB_SYSTEM_startButton_InLow_cwire), 
	.SC_STATEMACHINEPOINT_upButton_InLow(BB_SYSTEM_upButton_InLow_cwire), 
	.SC_STATEMACHINEPOINT_downButton_InLow(BB_SYSTEM_downButton_InLow_cwire), 
	.SC_STATEMACHINEPOINT_leftButton_InLow(BB_SYSTEM_leftButton_InLow_cwire), 
	.SC_STATEMACHINEPOINT_rightButton_InLow(BB_SYSTEM_rightButton_InLow_cwire), 
	.SC_STATEMACHINEPOINT_bottomsidecomparator_InLow(BOTTOMSIDECOMPARATOR_2_STATEMACHINEBACKG_bottomside_cwire),
	.SC_STATEMACHINEPOINT_collisioncomparator_InLow(SC_RegCollisionOut_u0)
);

//######################################################################
//#	BACKGROUND
//######################################################################
SC_RegHOUSETYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_7)) SC_RegBACKGTYPE_u7 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data7_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(RegPOINTTYPE_2_POINTMATRIX_data7_Out)
);
SC_RegBACKGTYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_6)) SC_RegBACKGTYPE_u6 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data6_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(DATA_FIXED_INITREGBACKG_0)
);
SC_RegBACKGTYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_5)) SC_RegBACKGTYPE_u5 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data5_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(DATA_FIXED_INITREGBACKG_0)
);
SC_RegBACKGTYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_4)) SC_RegBACKGTYPE_u4 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data4_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(DATA_FIXED_INITREGBACKG_0)
);
SC_RegBACKGTYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_3)) SC_RegBACKGTYPE_u3 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data3_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(DATA_FIXED_INITREGBACKG_0)
);
SC_RegBACKGTYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_2)) SC_RegBACKGTYPE_u2 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data2_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(DATA_FIXED_INITREGBACKG_0)
);
SC_RegBACKGTYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_1)) SC_RegBACKGTYPE_u1 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data1_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(DATA_FIXED_INITREGBACKG_0)
);
SC_RegBACKGTYPE #(.RegBACKGTYPE_DATAWIDTH(DATAWIDTH_BUS), .DATA_FIXED_INITREGBACKG(DATA_FIXED_INITREGBACKG_0)) SC_RegBACKGTYPE_u0 (
// port map - connection between master ports and signals/registers   
	.SC_RegBACKGTYPE_data_OutBUS(RegBACKGTYPE_2_BACKGMATRIX_data0_Out),
	.SC_RegBACKGTYPE_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_RegBACKGTYPE_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_RegBACKGTYPE_clear_InLow(STATEMACHINEBACKG_clear_cwire),	
	.SC_RegBACKGTYPE_load_InLow(STATEMACHINEBACKG_load_cwire),
	.SC_RegBACKGTYPE_shiftselection_In(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_RegBACKGTYPE_data_InBUS(DATA_FIXED_INITREGBACKG_0)
);
SC_STATEMACHINEBACKG SC_STATEMACHINEBACKG_u0 (
// port map - connection between master ports and signals/registers   
	.SC_STATEMACHINEBACKG_clear_OutLow(STATEMACHINEBACKG_clear_cwire), 
	.SC_STATEMACHINEBACKG_load_OutLow(STATEMACHINEBACKG_load_cwire), 
	.SC_STATEMACHINEBACKG_shiftselection_Out(STATEMACHINEBACKG_shiftselection_cwire),
	.SC_STATEMACHINEBACKG_upcount_out(STATEMACHINEBACKG_upcount_cwire),
	.SC_STATEMACHINEBACKG_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_STATEMACHINEBACKG_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_STATEMACHINEBACKG_startButton_InLow(BB_SYSTEM_startButton_InLow_cwire),
	.SC_STATEMACHINEBACKG_T0_InLow(SPEEDCOMPARATOR_2_STATEMACHINEBACKG_T0_cwire)
);

//#SPEED
SC_upSPEEDCOUNTER #(.upSPEEDCOUNTER_DATAWIDTH(PRESCALER_DATAWIDTH)) SC_upSPEEDCOUNTER_u0 (
// port map - connection between master ports and signals/registers   
	.SC_upSPEEDCOUNTER_data_OutBUS(upSPEEDCOUNTER_data_BUS_wire),
	.SC_upSPEEDCOUNTER_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_upSPEEDCOUNTER_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_upSPEEDCOUNTER_upcount_InLow(STATEMACHINEBACKG_upcount_cwire)
);

CC_SPEEDCOMPARATOR #(.SPEEDCOMPARATOR_DATAWIDTH(PRESCALER_DATAWIDTH)) CC_SPEEDCOMPARATOR_u0 (
	.CC_SPEEDCOMPARATOR_T0_OutLow(SPEEDCOMPARATOR_2_STATEMACHINEBACKG_T0_cwire),
	.CC_SPEEDCOMPARATOR_data_InBUS(upSPEEDCOUNTER_data_BUS_wire)
);



//########################
# COLLISION COMPARATOR. Esta es parte nueva del código que muestra las conexiones hechas en el BB_SYSTEM para que el código funcione. 
//########################


CC_COLLISIONCOMPARATOR #(.COLLISIONCOMPARATOR_DATAWIDTH(DATAWIDTH_BUS)) CC_COLLISIONCOMPARATOR_u0 (
	.CC_COLLISIONCOMPARATOR_collision_OutLow(SC_RegCollisionOut_u0),
	//OUTPUT CONECTAR!!
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u0(RegBACKGTYPE_2_BACKGMATRIX_data0_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u0(RegPOINTTYPE_2_POINTMATRIX_data0_Out),
	
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u1(RegBACKGTYPE_2_BACKGMATRIX_data1_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u1(RegPOINTTYPE_2_POINTMATRIX_data1_Out),
	
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u2(RegBACKGTYPE_2_BACKGMATRIX_data2_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u2(RegPOINTTYPE_2_POINTMATRIX_data2_Out),
	
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u3(RegBACKGTYPE_2_BACKGMATRIX_data3_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u3(RegPOINTTYPE_2_POINTMATRIX_data3_Out),
	
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u4(RegBACKGTYPE_2_BACKGMATRIX_data4_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u4(RegPOINTTYPE_2_POINTMATRIX_data4_Out),
	
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u5(RegBACKGTYPE_2_BACKGMATRIX_data5_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u5(RegPOINTTYPE_2_POINTMATRIX_data5_Out),
	
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u6(RegBACKGTYPE_2_BACKGMATRIX_data6_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u6(RegPOINTTYPE_2_POINTMATRIX_data6_Out),
	
	.CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u7(RegBACKGTYPE_2_BACKGMATRIX_data7_Out),
	.CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u7(RegPOINTTYPE_2_POINTMATRIX_data7_Out)
);

//######################################################################
//#	COMPARATOR END OF MATRIX (BOTTON SIDE)
//######################################################################
CC_BOTTOMSIDECOMPARATOR #(.BOTTOMSIDECOMPARATOR_DATAWIDTH(DATAWIDTH_BUS)) CC_BOTTOMSIDECOMPARATOR_u0 (
	.CC_BOTTOMSIDECOMPARATOR_bottomside_OutLow(BOTTOMSIDECOMPARATOR_2_STATEMACHINEBACKG_bottomside_cwire),
	.CC_BOTTOMSIDECOMPARATOR_data_InBUS(RegPOINTTYPE_2_POINTMATRIX_data0_Out)
);


//######################################################################
//#	TO LED MATRIZ: VISUALIZATION
//######################################################################
assign regGAME_data0_wire = RegPOINTTYPE_2_POINTMATRIX_data0_Out | RegBACKGTYPE_2_BACKGMATRIX_data0_Out;
assign regGAME_data1_wire = RegPOINTTYPE_2_POINTMATRIX_data1_Out | RegBACKGTYPE_2_BACKGMATRIX_data1_Out;
assign regGAME_data2_wire = RegPOINTTYPE_2_POINTMATRIX_data2_Out | RegBACKGTYPE_2_BACKGMATRIX_data2_Out;
assign regGAME_data3_wire = RegPOINTTYPE_2_POINTMATRIX_data3_Out | RegBACKGTYPE_2_BACKGMATRIX_data3_Out;
assign regGAME_data4_wire = RegPOINTTYPE_2_POINTMATRIX_data4_Out | RegBACKGTYPE_2_BACKGMATRIX_data4_Out;
assign regGAME_data5_wire = RegPOINTTYPE_2_POINTMATRIX_data5_Out | RegBACKGTYPE_2_BACKGMATRIX_data5_Out;
assign regGAME_data6_wire = RegPOINTTYPE_2_POINTMATRIX_data6_Out | RegBACKGTYPE_2_BACKGMATRIX_data6_Out;
assign regGAME_data7_wire = RegPOINTTYPE_2_POINTMATRIX_data7_Out | RegBACKGTYPE_2_BACKGMATRIX_data7_Out;


assign data_max = (add==3'b000)?{regGAME_data0_wire[7],regGAME_data1_wire[7],regGAME_data2_wire[7],regGAME_data3_wire[7],regGAME_data4_wire[7],regGAME_data5_wire[7],regGAME_data6_wire[7],regGAME_data7_wire[7]}:
						(add==3'b001)?{regGAME_data0_wire[6],regGAME_data1_wire[6],regGAME_data2_wire[6],regGAME_data3_wire[6],regGAME_data4_wire[6],regGAME_data5_wire[6],regGAME_data6_wire[6],regGAME_data7_wire[6]}:
						(add==3'b010)?{regGAME_data0_wire[5],regGAME_data1_wire[5],regGAME_data2_wire[5],regGAME_data3_wire[5],regGAME_data4_wire[5],regGAME_data5_wire[5],regGAME_data6_wire[5],regGAME_data7_wire[5]}:
						(add==3'b011)?{regGAME_data0_wire[4],regGAME_data1_wire[4],regGAME_data2_wire[4],regGAME_data3_wire[4],regGAME_data4_wire[4],regGAME_data5_wire[4],regGAME_data6_wire[4],regGAME_data7_wire[4]}:
						(add==3'b100)?{regGAME_data0_wire[3],regGAME_data1_wire[3],regGAME_data2_wire[3],regGAME_data3_wire[3],regGAME_data4_wire[3],regGAME_data5_wire[3],regGAME_data6_wire[3],regGAME_data7_wire[3]}:
						(add==3'b101)?{regGAME_data0_wire[2],regGAME_data1_wire[2],regGAME_data2_wire[2],regGAME_data3_wire[2],regGAME_data4_wire[2],regGAME_data5_wire[2],regGAME_data6_wire[2],regGAME_data7_wire[2]}:
						(add==3'b110)?{regGAME_data0_wire[1],regGAME_data1_wire[1],regGAME_data2_wire[1],regGAME_data3_wire[1],regGAME_data4_wire[1],regGAME_data5_wire[1],regGAME_data6_wire[1],regGAME_data7_wire[1]}:
										  {regGAME_data0_wire[0],regGAME_data1_wire[0],regGAME_data2_wire[0],regGAME_data3_wire[0],regGAME_data4_wire[0],regGAME_data5_wire[0],regGAME_data6_wire[0],regGAME_data7_wire[0]};
									 
matrix_ctrl matrix_ctrl_unit_0( 
.max7219_din(BB_SYSTEM_max7219DIN_Out),//max7219_din 
.max7219_ncs(BB_SYSTEM_max7219NCS_Out),//max7219_ncs 
.max7219_clk(BB_SYSTEM_max7219CLK_Out),//max7219_clk
.disp_data(data_max), 
.disp_addr(add),
.intensity(4'hA),
.clk(BB_SYSTEM_CLOCK_50),
.reset(BB_SYSTEM_RESET_InHigh) //~lowRst_System
 ); 
 
//~ imagen img1(
//~ .act_add(add), 
//~ .max_in(data_max) );

//~ SC_CTRLMATRIX SC_CTRLMATRIX_u0( 
//~ .SC_CTRLMATRIX_max7219DIN_Out(BB_SYSTEM_max7219DIN_Out),	//max7219_din 
//~ .SC_CTRLMATRIX_max7219NCS_out(BB_SYSTEM_max7219NCS_Out),	//max7219_ncs 
//~ .SC_CTRLMATRIX_max7219CLK_Out(BB_SYSTEM_max7219CLK_Out),	//max7219_clk
//~ .SC_CTRLMATRIX_dispdata(data_max), 
//~ .SC_CTRLMATRIX_dispaddr(add),
//~ .SC_CTRLMATRIX_intensity(4'hA),
//~ .SC_CTRLMATRIX_CLOCK_50(BB_SYSTEM_CLOCK_50),
//~ .SC_CTRLMATRIX_RESET_InHigh(~BB_SYSTEM_RESET_InHigh) 		//~lowRst_System
 //~ ); 
 
//~ SC_IMAGE SC_IMAGE_u0(
//~ .SC_IMAGE_actadd(add), 
//~ .SC_IMAGE_maxin(data_max) );

//######################################################################
//#	TO TEST
//######################################################################

assign BB_SYSTEM_startButton_Out = BB_SYSTEM_startButton_InLow_cwire;
assign BB_SYSTEM_upButton_Out = BB_SYSTEM_upButton_InLow_cwire;
assign BB_SYSTEM_downButton_Out = BB_SYSTEM_downButton_InLow_cwire;
assign BB_SYSTEM_leftButton_Out = BB_SYSTEM_leftButton_InLow_cwire;
assign BB_SYSTEM_rightButton_Out = BB_SYSTEM_rightButton_InLow_cwire;
//TO TEST
assign BB_SYSTEM_TEST0 = BB_SYSTEM_startButton_InLow_cwire;
assign BB_SYSTEM_TEST1 = BB_SYSTEM_startButton_InLow_cwire;
assign BB_SYSTEM_TEST2 = BB_SYSTEM_startButton_InLow_cwire;

//######################################################################
//#	TO 7SEG
//######################################################################

CC_BIN2BCD1 CC_BIN2BCD1_u0 (
// port map - connection between master ports and signals/registers   
	.CC_BIN2BCD_bcd_OutBUS(BIN2BCD1_2_SEVENSEG1_data_BUS_wire),
	.CC_BIN2BCD_bin_InBUS(upCOUNTER_2_BIN2BCD1_data_BUS_wire)
);

CC_SEVENSEG1 CC_SEVENSEG1_u0 (
// port map - connection between master ports and signals/registers   
	.CC_SEVENSEG1_an(BB_SYSTEM_display_OutBUS[11:8]),
	.CC_SEVENSEG1_a(BB_SYSTEM_display_OutBUS[0]),
	.CC_SEVENSEG1_b(BB_SYSTEM_display_OutBUS[1]),
	.CC_SEVENSEG1_c(BB_SYSTEM_display_OutBUS[2]),
	.CC_SEVENSEG1_d(BB_SYSTEM_display_OutBUS[3]),
	.CC_SEVENSEG1_e(BB_SYSTEM_display_OutBUS[4]),
	.CC_SEVENSEG1_f(BB_SYSTEM_display_OutBUS[5]),
	.CC_SEVENSEG1_g(BB_SYSTEM_display_OutBUS[6]),
	.CC_SEVENSEG1_dp(BB_SYSTEM_display_OutBUS[7]),
	.CC_SEVENSEG1_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.CC_SEVENSEG1_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.CC_SEVENSEG1_in0(BIN2BCD1_2_SEVENSEG1_data_BUS_wire[3:0]),
	.CC_SEVENSEG1_in1(BIN2BCD1_2_SEVENSEG1_data_BUS_wire[7:4]),
	.CC_SEVENSEG1_in2(BIN2BCD1_2_SEVENSEG1_data_BUS_wire[11:8]),
	.CC_SEVENSEG1_in3(BIN2BCD1_2_SEVENSEG1_data_BUS_wire[11:8])
);

SC_upCOUNTER #(.upCOUNTER_DATAWIDTH(DATAWIDTH_BUS)) SC_upCOUNTER_u0 (
// port map - connection between master ports and signals/registers   
	.SC_upCOUNTER_data_OutBUS(upCOUNTER_2_BIN2BCD1_data_BUS_wire),
	.SC_upCOUNTER_CLOCK_50(BB_SYSTEM_CLOCK_50),
	.SC_upCOUNTER_RESET_InHigh(BB_SYSTEM_RESET_InHigh),
	.SC_upCOUNTER_upcount_InLow(STATEMACHINEPOINT_load0_cwire)
);

endmodule
# El registro de HOUSE que muestra como se maneja las casas del frogger y como se queda encendida la luz
//======================================================
//  MODULE Definition
//=======================================================
module SC_RegHOUSETYPE #(parameter RegBACKGTYPE_DATAWIDTH=8, parameter DATA_FIXED_INITREGBACKG=8'b00000000)(
	//////////// OUTPUTS //////////
	SC_RegBACKGTYPE_data_OutBUS,
	SC_RegHOUSETYPE_data_winOutBus,
	//////////// INPUTS //////////
	SC_RegBACKGTYPE_CLOCK_50,
	SC_RegBACKGTYPE_RESET_InHigh,
	SC_RegBACKGTYPE_clear_InLow, 
	SC_RegBACKGTYPE_load_InLow, 
	SC_RegBACKGTYPE_shiftselection_In,
	SC_RegBACKGTYPE_data_InBUS,
	//
	SC_RegHOUSETYPE_collision_InLow,
	SC_RegHOUSETYPE_sum_InBus
);
//=======================================================
//  PARAMETER declarations
//=======================================================

//=======================================================
//  PORT declarations
//=======================================================
output		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_OutBUS;
output      [1:0] SC_RegHOUSETYPE_data_winOutBus;

input		SC_RegBACKGTYPE_CLOCK_50;
input		SC_RegBACKGTYPE_RESET_InHigh;
input		SC_RegBACKGTYPE_clear_InLow;
input		SC_RegBACKGTYPE_load_InLow;	
input		[1:0] SC_RegBACKGTYPE_shiftselection_In;
input		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_InBUS;
input    SC_RegHOUSETYPE_collision_InLow;
input    SC_RegHOUSETYPE_sum_InBus;

//=======================================================
//  REG/WIRE declarations
//=======================================================
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Register;
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Signal;
reg [1:0] RegHOUSETYPE_Signal;
reg [1:0] RegHOUSETYPE_Register;
//=======================================================
//  Structural coding
//=======================================================
//INPUT LOGIC: COMBINATIONAL
always @(*)
begin
	if (SC_RegBACKGTYPE_clear_InLow == 1'b0)
		RegBACKGTYPE_Signal = DATA_FIXED_INITREGBACKG;
	
	else if (SC_RegBACKGTYPE_load_InLow == 1'b0)
		if (SC_RegHOUSETYPE_collision_InLow == 1'b1)
				RegBACKGTYPE_Signal = SC_RegHOUSETYPE_sum_InBus;
	else
		RegBACKGTYPE_Signal = RegBACKGTYPE_Register;
	end
always @(*)
begin
	if (RegBACKGTYPE_Signal == 8'b11111111)
		RegHOUSETYPE_Signal = 2'b11;
	else if (RegBACKGTYPE_Signal > RegBACKGTYPE_Register)
		RegHOUSETYPE_Signal = 2'b01;
	else
		RegHOUSETYPE_Signal = 2'b00;
end	
//STATE REGISTER: SEQUENTIAL
always @(posedge SC_RegBACKGTYPE_CLOCK_50, posedge SC_RegBACKGTYPE_RESET_InHigh)
begin
	if (SC_RegBACKGTYPE_RESET_InHigh == 1'b1)
		RegBACKGTYPE_Register <= 0;
	else
		RegBACKGTYPE_Register <= RegBACKGTYPE_Signal;
end
always @(posedge SC_RegBACKGTYPE_CLOCK_50, posedge SC_RegBACKGTYPE_RESET_InHigh)
begin
	if (SC_RegBACKGTYPE_RESET_InHigh == 1'b1)
		RegHOUSETYPE_Register <= 0;
	else
		RegHOUSETYPE_Register <= RegHOUSETYPE_Signal;
end

//=======================================================
//  Outputs
//=======================================================
//OUTPUT LOGIC: COMBINATIONAL
assign SC_RegBACKGTYPE_data_OutBUS = RegBACKGTYPE_Register;
assign SC_RegHOUSETYPE_data_winOutBus = RegHOUSETYPE_Register;

endmodule
# Ejemplo de un registro Frogger
//=======================================================
//  MODULE Definition
//=======================================================
module SC_RegBACKGTYPE #(parameter RegBACKGTYPE_DATAWIDTH=8, parameter DATA_FIXED_INITREGBACKG=8'b00000000)(
	//////////// OUTPUTS //////////
	SC_RegBACKGTYPE_data_OutBUS,
	//////////// INPUTS //////////
	SC_RegBACKGTYPE_CLOCK_50,
	SC_RegBACKGTYPE_RESET_InHigh,
	SC_RegBACKGTYPE_clear_InLow, 
	SC_RegBACKGTYPE_load_InLow, 
	SC_RegBACKGTYPE_shiftselection_In,
	SC_RegBACKGTYPE_data_InBUS
);
//=======================================================
//  PARAMETER declarations
//=======================================================

//=======================================================
//  PORT declarations
//=======================================================
output		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_OutBUS;
input		SC_RegBACKGTYPE_CLOCK_50;
input		SC_RegBACKGTYPE_RESET_InHigh;
input		SC_RegBACKGTYPE_clear_InLow;
input		SC_RegBACKGTYPE_load_InLow;	
input		[1:0] SC_RegBACKGTYPE_shiftselection_In;
input		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_InBUS;

//=======================================================
//  REG/WIRE declarations
//=======================================================
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Register;
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Signal;
//=======================================================
//  Structural coding
//=======================================================
//INPUT LOGIC: COMBINATIONAL
always @(*)
begin
	if (SC_RegBACKGTYPE_clear_InLow == 1'b0)
		RegBACKGTYPE_Signal = DATA_FIXED_INITREGBACKG;
	else if (SC_RegBACKGTYPE_load_InLow == 1'b0)
		RegBACKGTYPE_Signal = SC_RegBACKGTYPE_data_InBUS;
	else if (SC_RegBACKGTYPE_shiftselection_In == 2'b01)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-2:0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1]};
	else if (SC_RegBACKGTYPE_shiftselection_In== 2'b10)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1:1]};
	else
		RegBACKGTYPE_Signal = RegBACKGTYPE_Register;
	end	
//STATE REGISTER: SEQUENTIAL
always @(posedge SC_RegBACKGTYPE_CLOCK_50, posedge SC_RegBACKGTYPE_RESET_InHigh)
begin
	if (SC_RegBACKGTYPE_RESET_InHigh == 1'b1)
		RegBACKGTYPE_Register <= 0;
	else
		RegBACKGTYPE_Register <= RegBACKGTYPE_Signal;
end
//=======================================================
//  Outputs
//=======================================================
//OUTPUT LOGIC: COMBINATIONAL
assign SC_RegBACKGTYPE_data_OutBUS = RegBACKGTYPE_Register;

endmodule

# Ejemplo Registro House
//=======================================================
//  MODULE Definition
//=======================================================
module SC_RegBACKGTYPE #(parameter RegBACKGTYPE_DATAWIDTH=8, parameter DATA_FIXED_INITREGBACKG=8'b00000000)(
	//////////// OUTPUTS //////////
	SC_RegBACKGTYPE_data_OutBUS,
	//////////// INPUTS //////////
	SC_RegBACKGTYPE_CLOCK_50,
	SC_RegBACKGTYPE_RESET_InHigh,
	SC_RegBACKGTYPE_clear_InLow, 
	SC_RegBACKGTYPE_load_InLow, 
	SC_RegBACKGTYPE_shiftselection_In,
	SC_RegBACKGTYPE_data_InBUS
);
//=======================================================
//  PARAMETER declarations
//=======================================================

//=======================================================
//  PORT declarations
//=======================================================
output		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_OutBUS;
input		SC_RegBACKGTYPE_CLOCK_50;
input		SC_RegBACKGTYPE_RESET_InHigh;
input		SC_RegBACKGTYPE_clear_InLow;
input		SC_RegBACKGTYPE_load_InLow;	
input		[1:0] SC_RegBACKGTYPE_shiftselection_In;
input		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_InBUS;

//=======================================================
//  REG/WIRE declarations
//=======================================================
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Register;
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Signal;
//=======================================================
//  Structural coding
//=======================================================
//INPUT LOGIC: COMBINATIONAL
always @(*)
begin
	if (SC_RegBACKGTYPE_clear_InLow == 1'b0)
		RegBACKGTYPE_Signal = DATA_FIXED_INITREGBACKG;
	else if (SC_RegBACKGTYPE_load_InLow == 1'b0)
		RegBACKGTYPE_Signal = SC_RegBACKGTYPE_data_InBUS;
	else if (SC_RegBACKGTYPE_shiftselection_In == 2'b01)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-2:0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1]};
	else if (SC_RegBACKGTYPE_shiftselection_In== 2'b10)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1:1]};
	else
		RegBACKGTYPE_Signal = RegBACKGTYPE_Register;
	end	
//STATE REGISTER: SEQUENTIAL
always @(posedge SC_RegBACKGTYPE_CLOCK_50, posedge SC_RegBACKGTYPE_RESET_InHigh)
begin
	if (SC_RegBACKGTYPE_RESET_InHigh == 1'b1)
		RegBACKGTYPE_Register <= 0;
	else
		RegBACKGTYPE_Register <= RegBACKGTYPE_Signal;
end
//=======================================================
//  Outputs
//=======================================================
//OUTPUT LOGIC: COMBINATIONAL
assign SC_RegBACKGTYPE_data_OutBUS = RegBACKGTYPE_Register;

endmodule


# Codigo de la funcionalidad de la colisión donde se evidencia la AND que se hace a todos los register 
module CC_COLLISIONCOMPARATOR #(parameter COLLISIONCOMPARATOR_DATAWIDTH=8)(
//////////// OUTPUTS //////////
	CC_COLLISIONCOMPARATOR_collision_OutLow,
//////////// INPUTS //////////
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u0,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u0,
	
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u1,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u1,
	
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u2,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u2,
	
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u3,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u3,
	
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u4,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u4,
	
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u5,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u5,
	
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u6,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u6,
	
	CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u7,
	CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u7,
);
//=======================================================
//  PARAMETER declarations
//=======================================================

//=======================================================
//  PORT declarations
//=======================================================
output	reg CC_COLLISIONCOMPARATOR_collision_OutLow;
input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u0;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u0;

input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u1;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u1;

input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u2;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u2;

input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u3;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u3;

input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u4;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u4;

input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u5;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u5;

input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u6;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u6;

input 	[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u7;
input		[COLLISIONCOMPARATOR_DATAWIDTH-1:0] CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u7;

//=======================================================
//  REG/WIRE declarations
//=======================================================
//=======================================================
//  Structural coding
//=======================================================
always @(*)
begin
	if( (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u0 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u0) == 8'b00000000 | (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u1 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u1) == 8'b00000000 | (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u2 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u2) == 8'b00000000 | (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u3 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u3) == 8'b00000000 | (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u4 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u4) == 8'b00000000 | (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u5 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u5) == 8'b00000000 | (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u6 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u6) == 8'b00000000 | (CC_COLLISIONCOMPARATOR_data_InBUS_POINT_u7 && CC_COLLISIONCOMPARATOR_data_InBUS_BACKG_u7) == 8'b00000000)
		CC_COLLISIONCOMPARATOR_collision_OutLow = 1'b1;
	else 
		CC_COLLISIONCOMPARATOR_collision_OutLow = 1'b0;
end

endmodule

# Comparador de velocidad donde se evidencia el cambio de velocidad que entra a la maquina de estados

//  MODULE Definition
//=======================================================
module CC_SPEEDCOMPARATOR #(parameter SPEEDCOMPARATOR_DATAWIDTH=23)(
//////////// OUTPUTS //////////
	CC_SPEEDCOMPARATOR_T0_OutLow,
//////////// INPUTS //////////
	CC_SPEEDCOMPARATOR_data_InBUS
);
//=======================================================
//  PARAMETER declarations
//=======================================================

//=======================================================
//  PORT declarations
//=======================================================
output	reg CC_SPEEDCOMPARATOR_T0_OutLow;
input 	[SPEEDCOMPARATOR_DATAWIDTH-1:0] CC_SPEEDCOMPARATOR_data_InBUS;
//=======================================================
//  REG/WIRE declarations
//=======================================================
//=======================================================
//  Structural coding
//=======================================================
always @(CC_SPEEDCOMPARATOR_data_InBUS)
begin
	if( CC_SPEEDCOMPARATOR_data_InBUS == 23'b11111111111111111111111)
		CC_SPEEDCOMPARATOR_T0_OutLow = 1'b0;
	else 
		CC_SPEEDCOMPARATOR_T0_OutLow = 1'b1;
end

endmodule


# Maquina de estado Frogger

//=======================================================
//  MODULE Definition
//=======================================================
module SC_RegBACKGTYPE #(parameter RegBACKGTYPE_DATAWIDTH=8, parameter DATA_FIXED_INITREGBACKG=8'b00000000)(
	//////////// OUTPUTS //////////
	SC_RegBACKGTYPE_data_OutBUS,
	//////////// INPUTS //////////
	SC_RegBACKGTYPE_CLOCK_50,
	SC_RegBACKGTYPE_RESET_InHigh,
	SC_RegBACKGTYPE_clear_InLow, 
	SC_RegBACKGTYPE_load_InLow, 
	SC_RegBACKGTYPE_shiftselection_In,
	SC_RegBACKGTYPE_data_InBUS
);
//=======================================================
//  PARAMETER declarations
//=======================================================

//=======================================================
//  PORT declarations
//=======================================================
output		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_OutBUS;
input		SC_RegBACKGTYPE_CLOCK_50;
input		SC_RegBACKGTYPE_RESET_InHigh;
input		SC_RegBACKGTYPE_clear_InLow;
input		SC_RegBACKGTYPE_load_InLow;	
input		[1:0] SC_RegBACKGTYPE_shiftselection_In;
input		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_InBUS;

//=======================================================
//  REG/WIRE declarations
//=======================================================
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Register;
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Signal;
//=======================================================
//  Structural coding
//=======================================================
//INPUT LOGIC: COMBINATIONAL
always @(*)
begin
	if (SC_RegBACKGTYPE_clear_InLow == 1'b0)
		RegBACKGTYPE_Signal = DATA_FIXED_INITREGBACKG;
	else if (SC_RegBACKGTYPE_load_InLow == 1'b0)
		RegBACKGTYPE_Signal = SC_RegBACKGTYPE_data_InBUS;
	else if (SC_RegBACKGTYPE_shiftselection_In == 2'b01)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-2:0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1]};
	else if (SC_RegBACKGTYPE_shiftselection_In== 2'b10)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1:1]};
	else
		RegBACKGTYPE_Signal = RegBACKGTYPE_Register;
	end	
//STATE REGISTER: SEQUENTIAL
always @(posedge SC_RegBACKGTYPE_CLOCK_50, posedge SC_RegBACKGTYPE_RESET_InHigh)
begin
	if (SC_RegBACKGTYPE_RESET_InHigh == 1'b1)
		RegBACKGTYPE_Register <= 0;
	else
		RegBACKGTYPE_Register <= RegBACKGTYPE_Signal;
end
//=======================================================
//  Outputs
//=======================================================
//OUTPUT LOGIC: COMBINATIONAL
assign SC_RegBACKGTYPE_data_OutBUS = RegBACKGTYPE_Register;

endmodule

# Maquina de Estados Background
//=======================================================
//  MODULE Definition
//=======================================================
module SC_RegBACKGTYPE #(parameter RegBACKGTYPE_DATAWIDTH=8, parameter DATA_FIXED_INITREGBACKG=8'b00000000)(
	//////////// OUTPUTS //////////
	SC_RegBACKGTYPE_data_OutBUS,
	//////////// INPUTS //////////
	SC_RegBACKGTYPE_CLOCK_50,
	SC_RegBACKGTYPE_RESET_InHigh,
	SC_RegBACKGTYPE_clear_InLow, 
	SC_RegBACKGTYPE_load_InLow, 
	SC_RegBACKGTYPE_shiftselection_In,
	SC_RegBACKGTYPE_data_InBUS
);
//=======================================================
//  PARAMETER declarations
//=======================================================

//=======================================================
//  PORT declarations
//=======================================================
output		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_OutBUS;
input		SC_RegBACKGTYPE_CLOCK_50;
input		SC_RegBACKGTYPE_RESET_InHigh;
input		SC_RegBACKGTYPE_clear_InLow;
input		SC_RegBACKGTYPE_load_InLow;	
input		[1:0] SC_RegBACKGTYPE_shiftselection_In;
input		[RegBACKGTYPE_DATAWIDTH-1:0]	SC_RegBACKGTYPE_data_InBUS;

//=======================================================
//  REG/WIRE declarations
//=======================================================
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Register;
reg [RegBACKGTYPE_DATAWIDTH-1:0] RegBACKGTYPE_Signal;
//=======================================================
//  Structural coding
//=======================================================
//INPUT LOGIC: COMBINATIONAL
always @(*)
begin
	if (SC_RegBACKGTYPE_clear_InLow == 1'b0)
		RegBACKGTYPE_Signal = DATA_FIXED_INITREGBACKG;
	else if (SC_RegBACKGTYPE_load_InLow == 1'b0)
		RegBACKGTYPE_Signal = SC_RegBACKGTYPE_data_InBUS;
	else if (SC_RegBACKGTYPE_shiftselection_In == 2'b01)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-2:0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1]};
	else if (SC_RegBACKGTYPE_shiftselection_In== 2'b10)
		RegBACKGTYPE_Signal = {RegBACKGTYPE_Register[0],RegBACKGTYPE_Register[RegBACKGTYPE_DATAWIDTH-1:1]};
	else
		RegBACKGTYPE_Signal = RegBACKGTYPE_Register;
	end	
//STATE REGISTER: SEQUENTIAL
always @(posedge SC_RegBACKGTYPE_CLOCK_50, posedge SC_RegBACKGTYPE_RESET_InHigh)
begin
	if (SC_RegBACKGTYPE_RESET_InHigh == 1'b1)
		RegBACKGTYPE_Register <= 0;
	else
		RegBACKGTYPE_Register <= RegBACKGTYPE_Signal;
end
//=======================================================
//  Outputs
//=======================================================
//OUTPUT LOGIC: COMBINATIONAL
assign SC_RegBACKGTYPE_data_OutBUS = RegBACKGTYPE_Register;

endmodule
