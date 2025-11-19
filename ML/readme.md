import React, { useState, useEffect } from 'react';
import { BarChart, Bar, ScatterChart, Scatter, LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer, Cell } from 'recharts';

const WineQualityAnalysis = () => {
  const [activeTab, setActiveTab] = useState('description');
  const [wineData, setWineData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Simulation de chargement des données Wine Quality
    const loadData = async () => {
      // Données simulées basées sur le dataset UCI Wine Quality
      const redWineStats = {
        samples: 1599,
        features: 11,
        qualityRange: [3, 8],
        meanQuality: 5.6,
        variables: [
          'fixed acidity',
          'volatile acidity',
          'citric acid',
          'residual sugar',
          'chlorides',
          'free sulfur dioxide',
          'total sulfur dioxide',
          'density',
          'pH',
          'sulphates',
          'alcohol'
        ]
      };

      const whiteWineStats = {
        samples: 4898,
        features: 11,
        qualityRange: [3, 9],
        meanQuality: 5.9,
        variables: [
          'fixed acidity',
          'volatile acidity',
          'citric acid',
          'residual sugar',
          'chlorides',
          'free sulfur dioxide',
          'total sulfur dioxide',
          'density',
          'pH',
          'sulphates',
          'alcohol'
        ]
      };

      // Distribution de qualité (simulée)
      const qualityDistribution = [
        { quality: 3, count: 30, percentage: 0.5 },
        { quality: 4, count: 216, percentage: 3.3 },
        { quality: 5, count: 2138, percentage: 32.8 },
        { quality: 6, count: 2836, percentage: 43.5 },
        { quality: 7, count: 1079, percentage: 16.6 },
        { quality: 8, count: 193, percentage: 3.0 },
        { quality: 9, count: 5, percentage: 0.1 }
      ];

      // Corrélations avec la qualité
      const correlations = [
        { feature: 'alcohol', correlation: 0.476, color: '#10b981' },
        { feature: 'sulphates', correlation: 0.251, color: '#10b981' },
        { feature: 'citric acid', correlation: 0.226, color: '#10b981' },
        { feature: 'fixed acidity', correlation: 0.124, color: '#10b981' },
        { feature: 'residual sugar', correlation: 0.014, color: '#94a3b8' },
        { feature: 'free sulfur dioxide', correlation: -0.051, color: '#94a3b8' },
        { feature: 'pH', correlation: -0.058, color: '#ef4444' },
        { feature: 'chlorides', correlation: -0.129, color: '#ef4444' },
        { feature: 'density', correlation: -0.175, color: '#ef4444' },
        { feature: 'total sulfur dioxide', correlation: -0.185, color: '#ef4444' },
        { feature: 'volatile acidity', correlation: -0.391, color: '#ef4444' }
      ].sort((a, b) => b.correlation - a.correlation);

      // Statistiques descriptives par feature
      const descriptiveStats = [
        { feature: 'alcohol', mean: 10.42, std: 1.07, min: 8.4, max: 14.9 },
        { feature: 'volatile acidity', mean: 0.53, std: 0.18, min: 0.12, max: 1.58 },
        { feature: 'citric acid', mean: 0.27, std: 0.19, min: 0.0, max: 1.0 },
        { feature: 'fixed acidity', mean: 8.32, std: 1.74, min: 4.6, max: 15.9 },
        { feature: 'pH', mean: 3.31, std: 0.15, min: 2.74, max: 4.01 }
      ];

      // Relation alcohol vs quality
      const alcoholQuality = [
        { alcohol: 9.0, quality: 5.2 },
        { alcohol: 9.5, quality: 5.3 },
        { alcohol: 10.0, quality: 5.5 },
        { alcohol: 10.5, quality: 5.7 },
        { alcohol: 11.0, quality: 5.9 },
        { alcohol: 11.5, quality: 6.1 },
        { alcohol: 12.0, quality: 6.3 },
        { alcohol: 12.5, quality: 6.4 },
        { alcohol: 13.0, quality: 6.5 }
      ];

      setWineData({
        redWineStats,
        whiteWineStats,
        qualityDistribution,
        correlations,
        descriptiveStats,
        alcoholQuality
      });
      setLoading(false);
    };

    loadData();
  }, []);

  if (loading) {
    return (
      <div className="flex items-center justify-center h-screen bg-gradient-to-br from-purple-50 to-pink-50">
        <div className="text-center">
          <div className="w-16 h-16 border-4 border-purple-500 border-t-transparent rounded-full animate-spin mx-auto mb-4"></div>
          <p className="text-gray-600 font-medium">Chargement des données...</p>
        </div>
      </div>
    );
  }

  const tabs = [
    { id: 'description', label: 'Description BDD', icon: '📊' },
    { id: 'analysis', label: 'Analyse Statistique', icon: '📈' },
    { id: 'correlations', label: 'Corrélations', icon: '🔗' },
    { id: 'results', label: 'Résultats', icon: '✅' }
  ];

  return (
    <div className="min-h-screen bg-gradient-to-br from-purple-50 via-pink-50 to-orange-50 p-6">
      <div className="max-w-7xl mx-auto">
        {/* Header */}
        <div className="bg-white rounded-2xl shadow-xl p-8 mb-6 border-t-4 border-purple-500">
          <h1 className="text-4xl font-bold text-gray-800 mb-2">🍷 Analyse du Dataset Wine Quality</h1>
          <p className="text-gray-600">Compte rendu complet - UCI Machine Learning Repository</p>
          <div className="mt-4 flex gap-4 text-sm">
            <span className="px-4 py-2 bg-red-100 text-red-700 rounded-full font-medium">
              Vin Rouge: {wineData.redWineStats.samples} échantillons
            </span>
            <span className="px-4 py-2 bg-yellow-100 text-yellow-700 rounded-full font-medium">
              Vin Blanc: {wineData.whiteWineStats.samples} échantillons
            </span>
          </div>
        </div>

        {/* Navigation Tabs */}
        <div className="flex gap-2 mb-6 overflow-x-auto">
          {tabs.map(tab => (
            <button
              key={tab.id}
              onClick={() => setActiveTab(tab.id)}
              className={`px-6 py-3 rounded-xl font-medium transition-all whitespace-nowrap ${
                activeTab === tab.id
                  ? 'bg-purple-600 text-white shadow-lg transform scale-105'
                  : 'bg-white text-gray-600 hover:bg-gray-50'
              }`}
            >
              <span className="mr-2">{tab.icon}</span>
              {tab.label}
            </button>
          ))}
        </div>

        {/* Content */}
        <div className="bg-white rounded-2xl shadow-xl p-8">
          {activeTab === 'description' && (
            <div className="space-y-6">
              <h2 className="text-3xl font-bold text-gray-800 mb-4">📋 Description de la Base de Données</h2>
              
              <div className="bg-gradient-to-r from-purple-50 to-pink-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-gray-800 mb-3">🎯 Objectif du Dataset</h3>
                <p className="text-gray-700 leading-relaxed">
                  Le dataset <strong>Wine Quality</strong> est une collection de données physicochimiques et sensorielles 
                  sur les vins rouges et blancs portugais (Vinho Verde). L'objectif principal est de modéliser la qualité 
                  du vin en fonction de ses propriétés chimiques mesurables.
                </p>
              </div>

              <div className="grid md:grid-cols-2 gap-6">
                <div className="bg-red-50 p-6 rounded-xl border-l-4 border-red-500">
                  <h3 className="text-xl font-bold text-red-700 mb-3">🍷 Vin Rouge</h3>
                  <ul className="space-y-2 text-gray-700">
                    <li><strong>Échantillons:</strong> {wineData.redWineStats.samples}</li>
                    <li><strong>Variables:</strong> {wineData.redWineStats.features} features + 1 target</li>
                    <li><strong>Qualité moyenne:</strong> {wineData.redWineStats.meanQuality}/10</li>
                    <li><strong>Plage de qualité:</strong> {wineData.redWineStats.qualityRange[0]} - {wineData.redWineStats.qualityRange[1]}</li>
                  </ul>
                </div>

                <div className="bg-yellow-50 p-6 rounded-xl border-l-4 border-yellow-500">
                  <h3 className="text-xl font-bold text-yellow-700 mb-3">🥂 Vin Blanc</h3>
                  <ul className="space-y-2 text-gray-700">
                    <li><strong>Échantillons:</strong> {wineData.whiteWineStats.samples}</li>
                    <li><strong>Variables:</strong> {wineData.whiteWineStats.features} features + 1 target</li>
                    <li><strong>Qualité moyenne:</strong> {wineData.whiteWineStats.meanQuality}/10</li>
                    <li><strong>Plage de qualité:</strong> {wineData.whiteWineStats.qualityRange[0]} - {wineData.whiteWineStats.qualityRange[1]}</li>
                  </ul>
                </div>
              </div>

              <div className="bg-blue-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-blue-700 mb-3">🔬 Variables Physicochimiques (Features)</h3>
                <div className="grid md:grid-cols-2 gap-4">
                  {wineData.redWineStats.variables.map((variable, idx) => (
                    <div key={idx} className="flex items-center gap-2">
                      <span className="w-2 h-2 bg-blue-500 rounded-full"></span>
                      <span className="text-gray-700 font-medium">{variable}</span>
                    </div>
                  ))}
                </div>
              </div>

              <div className="bg-green-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-green-700 mb-3">🎯 Variable Cible (Target)</h3>
                <p className="text-gray-700"><strong>quality:</strong> Score de qualité entre 0 et 10 (dans la pratique: 3-9) basé sur l'évaluation sensorielle de dégustateurs experts.</p>
              </div>

              <div className="bg-orange-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-orange-700 mb-3">📖 Source et Citation</h3>
                <p className="text-gray-700 mb-2">
                  <strong>Créateurs:</strong> Paulo Cortez, António Cerdeira, Fernando Almeida, Telmo Matos, José Reis
                </p>
                <p className="text-gray-700 text-sm italic">
                  P. Cortez, A. Cerdeira, F. Almeida, T. Matos and J. Reis. 
                  Modeling wine preferences by data mining from physicochemical properties. 
                  Decision Support Systems, Elsevier, 47(4):547-553, 2009.
                </p>
              </div>
            </div>
          )}

          {activeTab === 'analysis' && (
            <div className="space-y-6">
              <h2 className="text-3xl font-bold text-gray-800 mb-4">📊 Analyse Statistique</h2>

              <div className="bg-gradient-to-r from-blue-50 to-cyan-50 p-6 rounded-xl mb-6">
                <h3 className="text-xl font-bold text-gray-800 mb-4">📈 Distribution de la Qualité</h3>
                <ResponsiveContainer width="100%" height={300}>
                  <BarChart data={wineData.qualityDistribution}>
                    <CartesianGrid strokeDasharray="3 3" stroke="#e5e7eb" />
                    <XAxis dataKey="quality" label={{ value: 'Qualité', position: 'insideBottom', offset: -5 }} />
                    <YAxis label={{ value: 'Nombre d\'échantillons', angle: -90, position: 'insideLeft' }} />
                    <Tooltip 
                      contentStyle={{ backgroundColor: '#fff', border: '2px solid #8b5cf6', borderRadius: '8px' }}
                      formatter={(value, name) => [
                        name === 'count' ? `${value} échantillons` : `${value}%`,
                        name === 'count' ? 'Nombre' : 'Pourcentage'
                      ]}
                    />
                    <Legend />
                    <Bar dataKey="count" fill="#8b5cf6" radius={[8, 8, 0, 0]} />
                  </BarChart>
                </ResponsiveContainer>
                <p className="text-gray-700 mt-4">
                  <strong>Observation:</strong> La distribution est approximativement normale, centrée autour des qualités 5-6. 
                  Les vins de qualité extrême (3, 9) sont rares, représentant moins de 1% du dataset.
                </p>
              </div>

              <div className="bg-gradient-to-r from-green-50 to-emerald-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-gray-800 mb-4">📋 Statistiques Descriptives (Top 5 Features)</h3>
                <div className="overflow-x-auto">
                  <table className="w-full text-left">
                    <thead className="bg-green-100">
                      <tr>
                        <th className="px-4 py-3 font-bold text-green-800">Feature</th>
                        <th className="px-4 py-3 font-bold text-green-800">Moyenne</th>
                        <th className="px-4 py-3 font-bold text-green-800">Écart-type</th>
                        <th className="px-4 py-3 font-bold text-green-800">Min</th>
                        <th className="px-4 py-3 font-bold text-green-800">Max</th>
                      </tr>
                    </thead>
                    <tbody>
                      {wineData.descriptiveStats.map((stat, idx) => (
                        <tr key={idx} className="border-b border-green-100 hover:bg-green-50 transition">
                          <td className="px-4 py-3 font-medium text-gray-800">{stat.feature}</td>
                          <td className="px-4 py-3 text-gray-700">{stat.mean.toFixed(2)}</td>
                          <td className="px-4 py-3 text-gray-700">{stat.std.toFixed(2)}</td>
                          <td className="px-4 py-3 text-gray-700">{stat.min.toFixed(2)}</td>
                          <td className="px-4 py-3 text-gray-700">{stat.max.toFixed(2)}</td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                </div>
              </div>

              <div className="grid md:grid-cols-2 gap-6">
                <div className="bg-purple-50 p-6 rounded-xl">
                  <h3 className="text-lg font-bold text-purple-700 mb-3">🔍 Insights Clés</h3>
                  <ul className="space-y-2 text-gray-700">
                    <li>✓ Dataset équilibré avec 6,497 échantillons total</li>
                    <li>✓ Aucune valeur manquante</li>
                    <li>✓ Variables continues bien distribuées</li>
                    <li>✓ Qualité majoritairement moyenne (5-6)</li>
                  </ul>
                </div>

                <div className="bg-pink-50 p-6 rounded-xl">
                  <h3 className="text-lg font-bold text-pink-700 mb-3">⚠️ Points d'Attention</h3>
                  <ul className="space-y-2 text-gray-700">
                    <li>⚠ Peu d'échantillons de qualité extrême</li>
                    <li>⚠ Déséquilibre blanc/rouge (3:1)</li>
                    <li>⚠ Échelle de qualité subjective</li>
                    <li>⚠ Variables potentiellement corrélées</li>
                  </ul>
                </div>
              </div>
            </div>
          )}

          {activeTab === 'correlations' && (
            <div className="space-y-6">
              <h2 className="text-3xl font-bold text-gray-800 mb-4">🔗 Analyse des Corrélations</h2>

              <div className="bg-gradient-to-r from-indigo-50 to-purple-50 p-6 rounded-xl mb-6">
                <h3 className="text-xl font-bold text-gray-800 mb-4">📊 Corrélation avec la Qualité (Coefficient de Pearson)</h3>
                <ResponsiveContainer width="100%" height={400}>
                  <BarChart 
                    data={wineData.correlations} 
                    layout="vertical"
                    margin={{ top: 5, right: 30, left: 150, bottom: 5 }}
                  >
                    <CartesianGrid strokeDasharray="3 3" stroke="#e5e7eb" />
                    <XAxis type="number" domain={[-0.5, 0.5]} />
                    <YAxis dataKey="feature" type="category" width={140} />
                    <Tooltip 
                      contentStyle={{ backgroundColor: '#fff', border: '2px solid #8b5cf6', borderRadius: '8px' }}
                      formatter={(value) => value.toFixed(3)}
                    />
                    <Bar dataKey="correlation" radius={[0, 8, 8, 0]}>
                      {wineData.correlations.map((entry, index) => (
                        <Cell key={`cell-${index}`} fill={entry.color} />
                      ))}
                    </Bar>
                  </BarChart>
                </ResponsiveContainer>
              </div>

              <div className="grid md:grid-cols-3 gap-4 mb-6">
                <div className="bg-green-50 p-4 rounded-xl border-l-4 border-green-500">
                  <h4 className="font-bold text-green-700 mb-2">✅ Corrélation Positive</h4>
                  <p className="text-sm text-gray-700">Coefficient &gt; 0.2</p>
                  <p className="text-xs text-gray-600 mt-2">Ces variables augmentent avec la qualité</p>
                </div>
                <div className="bg-gray-50 p-4 rounded-xl border-l-4 border-gray-400">
                  <h4 className="font-bold text-gray-700 mb-2">➖ Corrélation Faible</h4>
                  <p className="text-sm text-gray-700">-0.2 &lt; Coefficient &lt; 0.2</p>
                  <p className="text-xs text-gray-600 mt-2">Impact négligeable sur la qualité</p>
                </div>
                <div className="bg-red-50 p-4 rounded-xl border-l-4 border-red-500">
                  <h4 className="font-bold text-red-700 mb-2">❌ Corrélation Négative</h4>
                  <p className="text-sm text-gray-700">Coefficient &lt; -0.2</p>
                  <p className="text-xs text-gray-600 mt-2">Ces variables diminuent avec la qualité</p>
                </div>
              </div>

              <div className="bg-gradient-to-r from-orange-50 to-yellow-50 p-6 rounded-xl mb-6">
                <h3 className="text-xl font-bold text-gray-800 mb-4">🍾 Relation Alcool - Qualité</h3>
                <ResponsiveContainer width="100%" height={300}>
                  <ScatterChart margin={{ top: 20, right: 20, bottom: 20, left: 20 }}>
                    <CartesianGrid strokeDasharray="3 3" stroke="#e5e7eb" />
                    <XAxis 
                      dataKey="alcohol" 
                      name="Alcool" 
                      label={{ value: 'Taux d\'alcool (%)', position: 'insideBottom', offset: -5 }}
                    />
                    <YAxis 
                      dataKey="quality" 
                      name="Qualité" 
                      label={{ value: 'Qualité', angle: -90, position: 'insideLeft' }}
                    />
                    <Tooltip 
                      cursor={{ strokeDasharray: '3 3' }}
                      contentStyle={{ backgroundColor: '#fff', border: '2px solid #f59e0b', borderRadius: '8px' }}
                    />
                    <Scatter 
                      data={wineData.alcoholQuality} 
                      fill="#f59e0b" 
                      line={{ stroke: '#f59e0b', strokeWidth: 2 }}
                      lineType="fitting"
                    />
                  </ScatterChart>
                </ResponsiveContainer>
                <p className="text-gray-700 mt-4">
                  <strong>Interprétation:</strong> L'alcool présente la corrélation positive la plus forte (r = 0.476). 
                  Les vins avec un taux d'alcool plus élevé tendent à recevoir de meilleures notes de qualité.
                </p>
              </div>

              <div className="bg-blue-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-blue-700 mb-3">💡 Insights des Corrélations</h3>
                <div className="space-y-3 text-gray-700">
                  <div className="flex gap-2">
                    <span className="text-2xl">🏆</span>
                    <div>
                      <strong>Alcohol (r = 0.476):</strong> Corrélation positive la plus forte. Les vins avec plus d'alcool 
                      sont perçus comme de meilleure qualité, possiblement lié à la richesse et au corps du vin.
                    </div>
                  </div>
                  <div className="flex gap-2">
                    <span className="text-2xl">⚗️</span>
                    <div>
                      <strong>Sulphates (r = 0.251):</strong> Les sulfates agissent comme conservateurs et antioxydants, 
                      contribuant à la fraîcheur et à la longévité du vin.
                    </div>
                  </div>
                  <div className="flex gap-2">
                    <span className="text-2xl">🍋</span>
                    <div>
                      <strong>Citric Acid (r = 0.226):</strong> Ajoute de la fraîcheur et de la complexité aromatique, 
                      particulièrement apprécié dans les vins de qualité.
                    </div>
                  </div>
                  <div className="flex gap-2">
                    <span className="text-2xl">⚠️</span>
                    <div>
                      <strong>Volatile Acidity (r = -0.391):</strong> Corrélation négative importante. Une acidité volatile 
                      élevée indique une fermentation acétique indésirable, donnant un goût de vinaigre.
                    </div>
                  </div>
                </div>
              </div>
            </div>
          )}

          {activeTab === 'results' && (
            <div className="space-y-6">
              <h2 className="text-3xl font-bold text-gray-800 mb-4">✅ Résultats et Conclusions</h2>

              <div className="bg-gradient-to-r from-green-50 to-emerald-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-green-700 mb-3">🎯 Résultats Principaux</h3>
                <div className="space-y-3 text-gray-700">
                  <p>
                    <strong>1. Prédictibilité de la Qualité:</strong> La qualité du vin peut être modélisée avec une précision 
                    raisonnable (60-70%) en utilisant uniquement les propriétés physicochimiques, sans avoir besoin de dégustateurs.
                  </p>
                  <p>
                    <strong>2. Facteurs Clés de Qualité:</strong> Les trois variables les plus importantes sont l'alcool (positif), 
                    l'acidité volatile (négatif), et les sulfates (positif).
                  </p>
                  <p>
                    <strong>3. Complexité de la Qualité:</strong> La qualité du vin est un phénomène multifactoriel. Aucune 
                    variable seule ne peut prédire la qualité avec précision élevée (corrélation max: 0.476).
                  </p>
                </div>
              </div>

              <div className="grid md:grid-cols-2 gap-6">
                <div className="bg-blue-50 p-6 rounded-xl">
                  <h3 className="text-lg font-bold text-blue-700 mb-3">✨ Points Forts du Dataset</h3>
                  <ul className="space-y-2 text-gray-700">
                    <li>✓ Large taille d'échantillon (6,497)</li>
                    <li>✓ Données réelles et mesurables</li>
                    <li>✓ Aucune valeur manquante</li>
                    <li>✓ Variables bien documentées</li>
                    <li>✓ Applicable à l'industrie vinicole</li>
                    <li>✓ Évaluation par experts qualifiés</li>
                  </ul>
                </div>

                <div className="bg-orange-50 p-6 rounded-xl">
                  <h3 className="text-lg font-bold text-orange-700 mb-3">⚠️ Limitations</h3>
                  <ul className="space-y-2 text-gray-700">
                    <li>⚠ Limité aux vins Vinho Verde portugais</li>
                    <li>⚠ Déséquilibre blanc/rouge</li>
                    <li>⚠ Peu d'échantillons de qualité extrême</li>
                    <li>⚠ Subjectivité de l'évaluation sensorielle</li>
                    <li>⚠ Manque de données temporelles</li>
                    <li>⚠ Pas d'informations sur les cépages</li>
                  </ul>
                </div>
              </div>

              <div className="bg-purple-50 p-6 rounded-xl">
                <h3 className="text-xl font-bold text-purple-700 mb-3">🤖 Applications Machine Learning</h3>
                <div className="grid md:grid-cols-2 gap-4">
                  <div>
                    <h4 className="font-bold text-gray-800 mb-2">Problèmes de Régression</h4>
                    <ul className="space-y-1 text-sm text-gray-700">
                      <li>• Prédire le score de qualité exact</li>
                      <li>• Utiliser Linear Regression, Random Forest</li>
                      <li>• Métriques: RMSE, MAE, R²</li>
                    </ul>
                  </div>
