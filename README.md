# hypothesis-testing-assignment- Q1

{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": []
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "id": "IqNSUdKyvPto"
      },
      "outputs": [],
      "source": [
        "import pandas as pd\n",
        "import numpy as np\n",
        "from scipy import stats\n",
        "from scipy.stats import norm\n"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# Load the dataset\n",
        "data=pd.read_csv('/content/Cutlets (2).csv')\n",
        "data.head()\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 206
        },
        "id": "0FKybHAXxJcF",
        "outputId": "6c8eb276-4978-40e6-a787-de23d41c36ad"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "   Unit A  Unit B\n",
              "0  6.8090  6.7703\n",
              "1  6.4376  7.5093\n",
              "2  6.9157  6.7300\n",
              "3  7.3012  6.7878\n",
              "4  7.4488  7.1522"
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-337c83be-f35d-4b8a-ad7c-9496f8e2c901\">\n",
              "    <div class=\"colab-df-container\">\n",
              "      <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Unit A</th>\n",
              "      <th>Unit B</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>6.8090</td>\n",
              "      <td>6.7703</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>6.4376</td>\n",
              "      <td>7.5093</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>6.9157</td>\n",
              "      <td>6.7300</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>7.3012</td>\n",
              "      <td>6.7878</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>7.4488</td>\n",
              "      <td>7.1522</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "      <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-337c83be-f35d-4b8a-ad7c-9496f8e2c901')\"\n",
              "              title=\"Convert this dataframe to an interactive table.\"\n",
              "              style=\"display:none;\">\n",
              "        \n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "       width=\"24px\">\n",
              "    <path d=\"M0 0h24v24H0V0z\" fill=\"none\"/>\n",
              "    <path d=\"M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z\"/><path d=\"M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z\"/>\n",
              "  </svg>\n",
              "      </button>\n",
              "      \n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      flex-wrap:wrap;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "      <script>\n",
              "        const buttonEl =\n",
              "          document.querySelector('#df-337c83be-f35d-4b8a-ad7c-9496f8e2c901 button.colab-df-convert');\n",
              "        buttonEl.style.display =\n",
              "          google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "        async function convertToInteractive(key) {\n",
              "          const element = document.querySelector('#df-337c83be-f35d-4b8a-ad7c-9496f8e2c901');\n",
              "          const dataTable =\n",
              "            await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                     [key], {});\n",
              "          if (!dataTable) return;\n",
              "\n",
              "          const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "            '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "            + ' to learn more about interactive tables.';\n",
              "          element.innerHTML = '';\n",
              "          dataTable['output_type'] = 'display_data';\n",
              "          await google.colab.output.renderOutput(dataTable, element);\n",
              "          const docLink = document.createElement('div');\n",
              "          docLink.innerHTML = docLinkHtml;\n",
              "          element.appendChild(docLink);\n",
              "        }\n",
              "      </script>\n",
              "    </div>\n",
              "  </div>\n",
              "  "
            ]
          },
          "metadata": {},
          "execution_count": 2
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "unitA=pd.Series(data.iloc[:,0])\n",
        "unitA\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "Kg0yBiBHxSsN",
        "outputId": "335a0adb-6a21-4576-e073-579afb5033c3"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0     6.8090\n",
              "1     6.4376\n",
              "2     6.9157\n",
              "3     7.3012\n",
              "4     7.4488\n",
              "5     7.3871\n",
              "6     6.8755\n",
              "7     7.0621\n",
              "8     6.6840\n",
              "9     6.8236\n",
              "10    7.3930\n",
              "11    7.5169\n",
              "12    6.9246\n",
              "13    6.9256\n",
              "14    6.5797\n",
              "15    6.8394\n",
              "16    6.5970\n",
              "17    7.2705\n",
              "18    7.2828\n",
              "19    7.3495\n",
              "20    6.9438\n",
              "21    7.1560\n",
              "22    6.5341\n",
              "23    7.2854\n",
              "24    6.9952\n",
              "25    6.8568\n",
              "26    7.2163\n",
              "27    6.6801\n",
              "28    6.9431\n",
              "29    7.0852\n",
              "30    6.7794\n",
              "31    7.2783\n",
              "32    7.1561\n",
              "33    7.3943\n",
              "34    6.9405\n",
              "Name: Unit A, dtype: float64"
            ]
          },
          "metadata": {},
          "execution_count": 3
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "unitB=pd.Series(data.iloc[:,1])\n",
        "unitB\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "F7lvq2D8xVT3",
        "outputId": "4b705fae-0d6f-4767-ffc7-7ed405ad35a3"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0     6.7703\n",
              "1     7.5093\n",
              "2     6.7300\n",
              "3     6.7878\n",
              "4     7.1522\n",
              "5     6.8110\n",
              "6     7.2212\n",
              "7     6.6606\n",
              "8     7.2402\n",
              "9     7.0503\n",
              "10    6.8810\n",
              "11    7.4059\n",
              "12    6.7652\n",
              "13    6.0380\n",
              "14    7.1581\n",
              "15    7.0240\n",
              "16    6.6672\n",
              "17    7.4314\n",
              "18    7.3070\n",
              "19    6.7478\n",
              "20    6.8889\n",
              "21    7.4220\n",
              "22    6.5217\n",
              "23    7.1688\n",
              "24    6.7594\n",
              "25    6.9399\n",
              "26    7.0133\n",
              "27    6.9182\n",
              "28    6.3346\n",
              "29    7.5459\n",
              "30    7.0992\n",
              "31    7.1180\n",
              "32    6.6965\n",
              "33    6.5780\n",
              "34    7.3875\n",
              "Name: Unit B, dtype: float64"
            ]
          },
          "metadata": {},
          "execution_count": 4
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# 2-sample 2-tail ttest:   stats.ttest_ind(array1,array2)     # ind -> independent samples\n",
        "p_value=stats.ttest_ind(unitA,unitB)\n",
        "p_value\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "Ruah_4zFxZmf",
        "outputId": "f935a889-36fc-4c59-ad31-9f75c8e84769"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Ttest_indResult(statistic=0.7228688704678063, pvalue=0.4722394724599501)"
            ]
          },
          "metadata": {},
          "execution_count": 5
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "p_value[1]     # 2-tail probability \n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "xzsM1SYBxdE1",
        "outputId": "b44681d0-436b-49f2-d30c-1c3dfa3d1320"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0.4722394724599501"
            ]
          },
          "metadata": {},
          "execution_count": 6
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# compare p_value with α = 0.05 (At 5% significance level)\n"
      ],
      "metadata": {
        "id": "IkspvaS_xhDG"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "1IkwQ0NQxjh5"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}
