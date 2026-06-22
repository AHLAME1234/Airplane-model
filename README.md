# Airplane-model
clc; close all; clearvars;

%% ===== DATASET #1 =======================================================
load('workspace_test0.mat')  % test0 = DATASET #1

% Preparing the sensitivity of sensors
Sens.Channel1 = par.SensForce;   % Force
Sens.Channel2 = par.SensAccRef;  % AccRef (non utilise ici)
Sens.Channel3 = par.SensAcc1;
Sens.Channel4 = par.SensAcc2;
Sens.Channel5 = par.SensAcc3;
Sens.Channel6 = par.SensAcc4;
Sens.Channel7 = par.SensAcc5;
Sens.Channel8 = par.SensAcc6;

% Lecture du fichier de temperature
[t_T1, T1] = read_temperature_file('T_DATASET1.dat');

% Organisation finale
DATA1.F   = Temp.TimeData(:,1) ./ Sens.Channel1;            % Force            [N]
DATA1.acc = [Temp.TimeData(:,3) ./ Sens.Channel3, ...      % 6 accelerometres [m/s^2]
             Temp.TimeData(:,4) ./ Sens.Channel4, ...
             Temp.TimeData(:,5) ./ Sens.Channel5, ...
             Temp.TimeData(:,6) ./ Sens.Channel6, ...
             Temp.TimeData(:,7) ./ Sens.Channel7, ...
             Temp.TimeData(:,8) ./ Sens.Channel8];
DATA1.t   = TimeData.time(:);                              % temps vibrations [s]
DATA1.Fs  = par.Fs;                                        % freq echant.     [Hz]
DATA1.T   = T1;                                            % 12 patches IR    [degC]
DATA1.t_T = t_T1;                                          % temps temperature[s]


%% ===== DATASET #2 =======================================================
load('workspace_test1.mat')

Sens.Channel1 = par.SensForce;
Sens.Channel2 = par.SensAccRef;
Sens.Channel3 = par.SensAcc1;
Sens.Channel4 = par.SensAcc2;
Sens.Channel5 = par.SensAcc3;
Sens.Channel6 = par.SensAcc4;
Sens.Channel7 = par.SensAcc5;
Sens.Channel8 = par.SensAcc6;

[t_T2, T2] = read_temperature_file('T_DATASET2.dat');

DATA2.F   = Temp.TimeData(:,1) ./ Sens.Channel1;
DATA2.acc = [Temp.TimeData(:,3) ./ Sens.Channel3, ...
             Temp.TimeData(:,4) ./ Sens.Channel4, ...
             Temp.TimeData(:,5) ./ Sens.Channel5, ...
             Temp.TimeData(:,6) ./ Sens.Channel6, ...
             Temp.TimeData(:,7) ./ Sens.Channel7, ...
             Temp.TimeData(:,8) ./ Sens.Channel8];
DATA2.t   = TimeData.time(:);
DATA2.Fs  = par.Fs;
DATA2.T   = T2;
DATA2.t_T = t_T2;


%% ===== Nettoyage ======
clearvars -except DATA1 DATA2
