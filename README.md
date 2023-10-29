# noise-control
noise control- Sound absorption
% Define the properties of the mineral wool panel
r = 9600; %  Specific flow resistivity in Ns/m4
thickness = 50e-3; % Thickness in meters

% Define the frequency range for the octave band
freq = [125, 250, 500, 1000,2000,4000]; % Frequency range from 125 Hz to 4000 Hz

% Define the speed of sound in air and the density of air
c0 = 343; % Speed of sound in air in m/s
rho0 = 1.2041; % Density of air in kg/m^3

% Preallocate arrays for the real and imaginary parts of Γa and Za
Gamma_a_real = zeros(size(freq));
Gamma_a_imag = zeros(size(freq));
Za_real = zeros(size(freq));
Za_imag = zeros(size(freq));

% Calculate Γa and Za for each frequency in the octave band
for i = 1:length(freq)
    % Calculate Γa
    Gamma_a = (2*pi*freq(i)/c0) * (1 + 10.8 * (10^3 * freq(i) * r)^-0.70 - 1j*10.3 * (10^3 * freq(i) * r)^-0.59);
    
    % Calculate Za
    Za = rho0 * c0 * (1 + 9.08 * (10^3 * freq(i) * r)^-0.75 - 1j*11.9 * (10^3 * freq(i) * r)^-0.73);
    
    % Store the real and imaginary parts of Γa and Za
    Gamma_a_real(i) = real(Gamma_a);
    Gamma_a_imag(i) = imag(Gamma_a);
    Za_real(i) = real(Za);
    Za_imag(i) = imag(Za);
end

% Create a table with the results
T = table(freq', Gamma_a_real', Gamma_a_imag', Za_real', Za_imag', 'VariableNames', {'Frequency', 'Gamma_a_real', 'Gamma_a_imag', 'Za_real', 'Za_imag'});
disp(T);
